---
title: "aaaMachine 學習建議 API 文件 |Microsoft 文件"
description: "建議引擎 hello Microsoft Azure Marketplace 中可用的 azure 機器學習建議 API 文件。"
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
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="1da34-103">Azure Machine Learning 建議 API 文件</span><span class="sxs-lookup"><span data-stu-id="1da34-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="1da34-104">您應該開始使用 hello 建議 API 認知服務，而不此版本。</span><span class="sxs-lookup"><span data-stu-id="1da34-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="1da34-105">hello 建議認知服務將會取代此服務，並將那里開發所有 hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="1da34-106">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="1da34-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="1da34-107">深入了解[移轉 toohello 新認知的服務](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="1da34-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="1da34-108">本文件說明 Microsoft Azure Machine Learning 建議 API。</span><span class="sxs-lookup"><span data-stu-id="1da34-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="1da34-109">1.一般概觀</span><span class="sxs-lookup"><span data-stu-id="1da34-109">1. General overview</span></span>
<span data-ttu-id="1da34-110">本文件是 API 參考。</span><span class="sxs-lookup"><span data-stu-id="1da34-110">This document is an API reference.</span></span> <span data-ttu-id="1da34-111">您應該開始與 hello 「 Azure 機器學習建議-快速啟動 」 文件。</span><span class="sxs-lookup"><span data-stu-id="1da34-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="1da34-112">hello Azure 機器學習建議 API 可以分成下列邏輯群組的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="1da34-113"><ins>限制</ins> - 建議 API 限制。</span><span class="sxs-lookup"><span data-stu-id="1da34-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="1da34-114"><ins>一般資訊</ins> - 驗證、服務 URI 和版本控制的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1da34-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="1da34-115"><ins>模型 Basic</ins> -Api 可讓您在模型上的 toodo hello 基本作業 （例如建立、 更新和刪除模型）。</span><span class="sxs-lookup"><span data-stu-id="1da34-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="1da34-116"><ins>模型進階</ins>-tooget 進階資料洞察能力 hello 模型可讓您的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1da34-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="1da34-117"><ins>建立商務規則的模型</ins>-toomanage 商務規則 hello 模型建議結果可讓您的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1da34-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="1da34-118"><ins>目錄</ins>-toodo 基本作業模型類別目錄可讓您的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1da34-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="1da34-119">類別目錄含有 hello hello 使用量資料的項目上的中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="1da34-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="1da34-120"><ins>功能</ins>-Api，可讓項目上的 tooget insights 入 hello 類別目錄以及 toouse 此資訊 toobuild 更好的建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="1da34-121"><ins>使用量資料</ins>-Api 可讓您 toodo hello 模型使用方式資料的基本作業。</span><span class="sxs-lookup"><span data-stu-id="1da34-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="1da34-122">Hello 基本表單中的使用量資料是由組 & #60; userId & #62; 包含的資料列所組成，& #60; itemId & #62;。</span><span class="sxs-lookup"><span data-stu-id="1da34-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="1da34-123"><ins>建置</ins>-Api，可讓您 tootrigger 模型建置並執行基本作業的相關的 toothis 建置。</span><span class="sxs-lookup"><span data-stu-id="1da34-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="1da34-124">您可以在獲得有價值的使用狀況資料之後，觸發模型組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="1da34-125"><ins>建議</ins>-Api 可讓您 tooconsume 建議模型的 hello 組建結束之後。</span><span class="sxs-lookup"><span data-stu-id="1da34-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="1da34-126"><ins>使用者資料</ins>-toofetch hello 使用者使用量資料的資訊可讓您的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1da34-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="1da34-127"><ins>通知</ins>-Api 可讓您在問題 tooreceive 通知相關 tooyour API 作業。</span><span class="sxs-lookup"><span data-stu-id="1da34-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="1da34-128">（例如，您要回報透過資料擷取和大部分的失敗處理 hello 事件的使用量資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="1da34-129">這將會引發錯誤通知。)</span><span class="sxs-lookup"><span data-stu-id="1da34-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="1da34-130">2.限制</span><span class="sxs-lookup"><span data-stu-id="1da34-130">2. Limitations</span></span>
* <span data-ttu-id="1da34-131">hello 的模型，每個訂用帳戶數目上限為 10。</span><span class="sxs-lookup"><span data-stu-id="1da34-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="1da34-132">hello 的每個模型的組建數目上限為 20。</span><span class="sxs-lookup"><span data-stu-id="1da34-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="1da34-133">hello 類別目錄可以保存的項目數目上限為 100000。</span><span class="sxs-lookup"><span data-stu-id="1da34-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="1da34-134">hello 會保留的使用方式點數目上限是 ~ 5,000,000。</span><span class="sxs-lookup"><span data-stu-id="1da34-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="1da34-135">如果要上傳新的或報告，將會刪除最舊的 hello。</span><span class="sxs-lookup"><span data-stu-id="1da34-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="1da34-136">hello 可以傳送 POST （例如匯入類別目錄資料，匯入使用量資料） 中的資料大小上限為 200 MB。</span><span class="sxs-lookup"><span data-stu-id="1da34-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="1da34-137">hello 取得建議可以要求的項目數目上限為 150。</span><span class="sxs-lookup"><span data-stu-id="1da34-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="1da34-138">3.API – 一般資訊</span><span class="sxs-lookup"><span data-stu-id="1da34-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="1da34-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-139">3.1.</span></span> <span data-ttu-id="1da34-140">驗證</span><span class="sxs-lookup"><span data-stu-id="1da34-140">Authentication</span></span>
<span data-ttu-id="1da34-141">請遵循 hello Microsoft Azure Marketplace 的指導方針，驗證。</span><span class="sxs-lookup"><span data-stu-id="1da34-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="1da34-142">hello marketplace 支援任一種 hello 基本或 OAuth 驗證方法。</span><span class="sxs-lookup"><span data-stu-id="1da34-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="1da34-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-143">3.2.</span></span> <span data-ttu-id="1da34-144">服務 URI</span><span class="sxs-lookup"><span data-stu-id="1da34-144">Service URI</span></span>
<span data-ttu-id="1da34-145">hello Azure 機器學習建議 Api 的 hello 服務根目錄 URI 是[這裡。](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="1da34-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="1da34-146">hello 完整服務 URI 表示使用 hello OData 規格的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="1da34-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-147">3.3.</span></span> <span data-ttu-id="1da34-148">API 版本</span><span class="sxs-lookup"><span data-stu-id="1da34-148">API version</span></span>
<span data-ttu-id="1da34-149">每個 API 呼叫會有 hello 結尾呼叫應該設定 too1.0 的 api 版本查詢參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="1da34-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="1da34-150">3.4.</span></span> <span data-ttu-id="1da34-151">識別碼會區分大小寫</span><span class="sxs-lookup"><span data-stu-id="1da34-151">IDs are case sensitive</span></span>
<span data-ttu-id="1da34-152">任何 hello Api，所傳回的識別碼會區分大小寫和後續的 API 呼叫中當做參數傳遞時應該如此使用。</span><span class="sxs-lookup"><span data-stu-id="1da34-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="1da34-153">例如，模型識別碼和目錄識別碼都會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="1da34-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="1da34-154">4.建議品質和冷項目</span><span class="sxs-lookup"><span data-stu-id="1da34-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="1da34-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-155">4.1.</span></span> <span data-ttu-id="1da34-156">建議品質</span><span class="sxs-lookup"><span data-stu-id="1da34-156">Recommendation quality</span></span>
<span data-ttu-id="1da34-157">建立建議模型通常是足夠 tooallow hello 系統 tooprovide 建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="1da34-158">不過，建議的品質而異，根據處理 hello 使用量 hello hello 類別目錄的涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="1da34-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="1da34-159">例如 hello 系統如果您有許多的陌生項目 （而不重要的使用方式的項目），必須提供的建議項目，或使用這類項目與建議的一個問題。</span><span class="sxs-lookup"><span data-stu-id="1da34-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="1da34-160">順序 tooovercome hello 陌生的項目問題，請在 hello 系統會允許 hello 使用 hello 項目 tooenhance hello 建議的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="1da34-161">此中繼資料是參考的 tooas 功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="1da34-162">典型的功能是書籍的作者或電影的演員。</span><span class="sxs-lookup"><span data-stu-id="1da34-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="1da34-163">功能是透過 hello 類別目錄的索引鍵/值字串 hello 形式提供。</span><span class="sxs-lookup"><span data-stu-id="1da34-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="1da34-164">Hello hello 類別目錄檔案的完整格式，請參閱 toohello[匯入類別目錄區段](#81-import-catalog-data)。</span><span class="sxs-lookup"><span data-stu-id="1da34-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="1da34-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-165">4.2.</span></span> <span data-ttu-id="1da34-166">排名組建</span><span class="sxs-lookup"><span data-stu-id="1da34-166">Rank build</span></span>
<span data-ttu-id="1da34-167">功能可以加強 hello 的建議模型，但是 toodo 還需要 hello 使用有意義的功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="1da34-168">為了這個目的，引入新的組建 - 排名組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="1da34-169">此組建將排名 hello 實用性的功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="1da34-170">有意義的功能為排名分數 2 以上的功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="1da34-171">了解哪些 hello 功能有意義，觸發建議組建 hello 清單 （或子清單） 的有意義的功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="1da34-172">這些功能的 hello 增強暖項目和陌生項目可能 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="1da34-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="1da34-173">在順序 toouse 暖項目，它們 hello`UseFeatureInModel`組建參數應該設定。</span><span class="sxs-lookup"><span data-stu-id="1da34-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="1da34-174">陌生項目順序 toouse 功能，在 hello`AllowColdItemPlacement`應啟用組建參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="1da34-175">附註： 您不可能 tooenable`AllowColdItemPlacement`不啟用`UseFeatureInModel`。</span><span class="sxs-lookup"><span data-stu-id="1da34-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="1da34-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-176">4.3.</span></span> <span data-ttu-id="1da34-177">建議推論</span><span class="sxs-lookup"><span data-stu-id="1da34-177">Recommendation reasoning</span></span>
<span data-ttu-id="1da34-178">建議推論是功能使用方式的另一個層面。</span><span class="sxs-lookup"><span data-stu-id="1da34-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="1da34-179">事實上，hello Azure 機器學習建議引擎就可以使用功能 tooprovide 建議說明 （也稱為</span><span class="sxs-lookup"><span data-stu-id="1da34-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="1da34-180">推理），在 hello 開頭 toomore 信心建議 hello 建議取用者的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="1da34-181">tooenable 推理，hello`AllowFeatureCorrelation`和`ReasoningFeatureList`參數應該在安裝程式先前 toorequesting 建議組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="1da34-182">5.模型基本操作</span><span class="sxs-lookup"><span data-stu-id="1da34-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="1da34-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-183">5.1.</span></span> <span data-ttu-id="1da34-184">建立模型</span><span class="sxs-lookup"><span data-stu-id="1da34-184">Create Model</span></span>
<span data-ttu-id="1da34-185">建立「建立模型」要求。</span><span class="sxs-lookup"><span data-stu-id="1da34-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="1da34-186">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-186">HTTP Method</span></span> | <span data-ttu-id="1da34-187">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-188">POST</span><span class="sxs-lookup"><span data-stu-id="1da34-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-189">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-190">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-190">Parameter Name</span></span> | <span data-ttu-id="1da34-191">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-192">modelName</span><span class="sxs-lookup"><span data-stu-id="1da34-192">modelName</span></span> |<span data-ttu-id="1da34-193">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="1da34-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="1da34-194">最大長度：20</span><span class="sxs-lookup"><span data-stu-id="1da34-194">Max length: 20</span></span> |
| <span data-ttu-id="1da34-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-195">apiVersion</span></span> |<span data-ttu-id="1da34-196">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-196">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-197">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-197">Request Body</span></span> |<span data-ttu-id="1da34-198">無</span><span class="sxs-lookup"><span data-stu-id="1da34-198">NONE</span></span> |

<span data-ttu-id="1da34-199">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-199">**Response**:</span></span>

<span data-ttu-id="1da34-200">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="1da34-201">`feed/entry/content/properties/id`-包含 hello 模型識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="1da34-202">**注意**：模型識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="1da34-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="1da34-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-203">OData XML</span></span>

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

### <a name="52-get-model"></a><span data-ttu-id="1da34-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-204">5.2.</span></span> <span data-ttu-id="1da34-205">取得模型</span><span class="sxs-lookup"><span data-stu-id="1da34-205">Get Model</span></span>
<span data-ttu-id="1da34-206">建立一個「取得模型」要求。</span><span class="sxs-lookup"><span data-stu-id="1da34-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="1da34-207">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-207">HTTP Method</span></span> | <span data-ttu-id="1da34-208">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-209">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="1da34-210">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-211">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-211">Parameter Name</span></span> | <span data-ttu-id="1da34-212">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-213">id</span><span class="sxs-lookup"><span data-stu-id="1da34-213">id</span></span> |<span data-ttu-id="1da34-214">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="1da34-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-215">apiVersion</span></span> |<span data-ttu-id="1da34-216">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-216">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-217">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-217">Request Body</span></span> |<span data-ttu-id="1da34-218">無</span><span class="sxs-lookup"><span data-stu-id="1da34-218">NONE</span></span> |

<span data-ttu-id="1da34-219">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-219">**Response**:</span></span>

<span data-ttu-id="1da34-220">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-220">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-221">您可以找到下列項目 hello hello 模型資料：</span><span class="sxs-lookup"><span data-stu-id="1da34-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="1da34-222">`feed/entry/content/properties/Id` - 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="1da34-223">`feed/entry/content/properties/Name` - 模型名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="1da34-224">`feed/entry/content/properties/Date` - 模型建立日期。</span><span class="sxs-lookup"><span data-stu-id="1da34-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="1da34-225">`feed/entry/content/properties/Status` - 模型狀態。</span><span class="sxs-lookup"><span data-stu-id="1da34-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="1da34-226">下列其中一種 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-226">One of hello following:</span></span>
  * <span data-ttu-id="1da34-227">Created - 模型已建立且不包含目錄和使用方式。</span><span class="sxs-lookup"><span data-stu-id="1da34-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="1da34-228">ReadyForBuild - 模型已建立且包含目錄和使用狀況。</span><span class="sxs-lookup"><span data-stu-id="1da34-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="1da34-229">`feed/entry/content/properties/HasActiveBuild`-代表 hello 模型已成功建立。</span><span class="sxs-lookup"><span data-stu-id="1da34-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="1da34-230">`feed/entry/content/properties/BuildId` - 模型的作用中組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="1da34-231">`feed/entry/content/properties/Mpr` - 模型的平均值百分位數排名 (MPR - 如需詳細資訊，請參閱 ModelInsight)。</span><span class="sxs-lookup"><span data-stu-id="1da34-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="1da34-232">`feed/entry/content/properties/UserName` - 模型的內部使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="1da34-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-233">OData XML</span></span>

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

### <a name="53----get-all-models"></a><span data-ttu-id="1da34-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-234">5.3.</span></span>    <span data-ttu-id="1da34-235">取得所有模型</span><span class="sxs-lookup"><span data-stu-id="1da34-235">Get All Models</span></span>
<span data-ttu-id="1da34-236">擷取 hello 目前使用者的所有機型。</span><span class="sxs-lookup"><span data-stu-id="1da34-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="1da34-237">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-237">HTTP Method</span></span> | <span data-ttu-id="1da34-238">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-239">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="1da34-240">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-241">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-241">Parameter Name</span></span> | <span data-ttu-id="1da34-242">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-243">apiVersion</span></span> |<span data-ttu-id="1da34-244">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-244">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-245">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-245">Request Body</span></span> |<span data-ttu-id="1da34-246">無</span><span class="sxs-lookup"><span data-stu-id="1da34-246">NONE</span></span> |

<span data-ttu-id="1da34-247">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-247">**Response**:</span></span>

<span data-ttu-id="1da34-248">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="1da34-249">`feed/entry/content/properties/Id` - 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="1da34-250">`feed/entry/content/properties/Name` - 模型名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="1da34-251">`feed/entry/content/properties/Date` - 模型建立日期。</span><span class="sxs-lookup"><span data-stu-id="1da34-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="1da34-252">`feed/entry/content/properties/Status` - 模型狀態。</span><span class="sxs-lookup"><span data-stu-id="1da34-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="1da34-253">下列其中一種 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-253">One of hello following:</span></span>
  * <span data-ttu-id="1da34-254">Created - 模型已建立且不包含目錄和使用方式。</span><span class="sxs-lookup"><span data-stu-id="1da34-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="1da34-255">ReadyForBuild - 模型已建立且包含目錄和使用狀況。</span><span class="sxs-lookup"><span data-stu-id="1da34-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="1da34-256">`feed/entry/content/properties/HasActiveBuild`-代表 hello 模型已成功建立。</span><span class="sxs-lookup"><span data-stu-id="1da34-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="1da34-257">`feed/entry/content/properties/BuildId` - 模型的作用中組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="1da34-258">`feed/entry/content/properties/Mpr` - 模型 MPR (如需詳細資訊，請參閱 ModelInsight)。</span><span class="sxs-lookup"><span data-stu-id="1da34-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="1da34-259">`feed/entry/content/properties/UserName` - 模型的內部使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="1da34-260">`feed/entry/content/properties/UsageFileNames` - 逗號分隔的模型使用狀況檔案清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="1da34-261">`feed/entry/content/properties/CatalogId` - 模型目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="1da34-262">`feed/entry/content/properties/Description` - 模型說明。</span><span class="sxs-lookup"><span data-stu-id="1da34-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="1da34-263">`feed/entry/content/properties/CatalogFileName` - 模型目錄檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="1da34-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-264">OData XML</span></span>

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

### <a name="54----update-model"></a><span data-ttu-id="1da34-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="1da34-265">5.4.</span></span>    <span data-ttu-id="1da34-266">更新模型</span><span class="sxs-lookup"><span data-stu-id="1da34-266">Update Model</span></span>
<span data-ttu-id="1da34-267">您可以更新 hello 模型描述或 hello 作用中的組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="1da34-268">
<ins>作用中組建識別碼</ins> - 每個模型的每個組建都有組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="1da34-269">hello 作用中的組建識別碼是模型的 hello 第一個成功的組建的每個新。</span><span class="sxs-lookup"><span data-stu-id="1da34-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="1da34-270">當您有使用中的組建 ID，而且請勿 hello 的其他組建相同的模型，您需要 tooexplicitly hello 預設組建識別碼如果您想要將它設定。</span><span class="sxs-lookup"><span data-stu-id="1da34-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="1da34-271">當您使用的建議事項，如果未指定您想 toouse，將會自動使用其中一種 hello 預設 hello 組建 ID。</span><span class="sxs-lookup"><span data-stu-id="1da34-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="1da34-272">這項機制可讓您的生產環境-toobuild 新模型中有推薦模型並測試它們，才能將它們提升 tooproduction 之後。</span><span class="sxs-lookup"><span data-stu-id="1da34-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="1da34-273">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-273">HTTP Method</span></span> | <span data-ttu-id="1da34-274">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-275">PUT</span><span class="sxs-lookup"><span data-stu-id="1da34-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="1da34-276">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-277">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-277">Parameter Name</span></span> | <span data-ttu-id="1da34-278">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-279">id</span><span class="sxs-lookup"><span data-stu-id="1da34-279">id</span></span> |<span data-ttu-id="1da34-280">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="1da34-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-281">apiVersion</span></span> |<span data-ttu-id="1da34-282">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-282">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-283">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="1da34-284">請注意 hello XML 標記的描述，並將 ActiveBuildId 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="1da34-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="1da34-285">如果您不想 tooset 描述或 ActiveBuildId，移除 hello 整個標記。</span><span class="sxs-lookup"><span data-stu-id="1da34-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="1da34-286">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-286">**Response**:</span></span>

<span data-ttu-id="1da34-287">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="1da34-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="1da34-288">5.5.</span></span>    <span data-ttu-id="1da34-289">刪除模型</span><span class="sxs-lookup"><span data-stu-id="1da34-289">Delete Model</span></span>
<span data-ttu-id="1da34-290">根據識別碼刪除現有的模型。</span><span class="sxs-lookup"><span data-stu-id="1da34-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="1da34-291">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-291">HTTP Method</span></span> | <span data-ttu-id="1da34-292">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-293">刪除</span><span class="sxs-lookup"><span data-stu-id="1da34-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="1da34-294">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-295">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-295">Parameter Name</span></span> | <span data-ttu-id="1da34-296">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-297">id</span><span class="sxs-lookup"><span data-stu-id="1da34-297">id</span></span> |<span data-ttu-id="1da34-298">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="1da34-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-299">apiVersion</span></span> |<span data-ttu-id="1da34-300">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-300">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-301">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-301">Request Body</span></span> |<span data-ttu-id="1da34-302">無</span><span class="sxs-lookup"><span data-stu-id="1da34-302">NONE</span></span> |

<span data-ttu-id="1da34-303">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-303">**Response**:</span></span>

<span data-ttu-id="1da34-304">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-304">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-305">OData XML</span></span>

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

## <a name="6-model-advanced"></a><span data-ttu-id="1da34-306">6.模型進階操作</span><span class="sxs-lookup"><span data-stu-id="1da34-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="1da34-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-307">6.1.</span></span>    <span data-ttu-id="1da34-308">模型資料深入了解</span><span class="sxs-lookup"><span data-stu-id="1da34-308">Model Data Insight</span></span>
<span data-ttu-id="1da34-309">傳回建立此模型中的 hello 使用量資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="1da34-310">僅適用於建議組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="1da34-311">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-311">HTTP Method</span></span> | <span data-ttu-id="1da34-312">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-313">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="1da34-314">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-315">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-315">Parameter Name</span></span> | <span data-ttu-id="1da34-316">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-317">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-317">modelId</span></span> |<span data-ttu-id="1da34-318">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-319">apiVersion</span></span> |<span data-ttu-id="1da34-320">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-320">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-321">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-321">Request Body</span></span> |<span data-ttu-id="1da34-322">無</span><span class="sxs-lookup"><span data-stu-id="1da34-322">NONE</span></span> |

<span data-ttu-id="1da34-323">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-323">**Response**:</span></span>

<span data-ttu-id="1da34-324">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-324">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-325">hello 資料是以屬性的集合傳回。</span><span class="sxs-lookup"><span data-stu-id="1da34-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="1da34-326">`feed/entry/id/content/properties/key`-保存 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="1da34-327">`feed/entry/id/content/properties/value`-保留 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="1da34-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="1da34-328">hello 下表描述每個索引鍵所代表的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="1da34-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="1da34-329">Key</span><span class="sxs-lookup"><span data-stu-id="1da34-329">Key</span></span> | <span data-ttu-id="1da34-330">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="1da34-331">AvgItemLength</span></span> |<span data-ttu-id="1da34-332">每個項目不同使用者的平均數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="1da34-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="1da34-333">AvgUserLength</span></span> |<span data-ttu-id="1da34-334">每個使用者不同項目的平均數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="1da34-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="1da34-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="1da34-336">剪除不能模型化的項目之後的項目數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="1da34-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="1da34-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="1da34-338">剪除不能模型化的使用者和項目之後的始用點數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="1da34-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="1da34-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="1da34-340">剪除不能模型化的使用者和項目之後的始用點數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="1da34-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="1da34-341">MaxItemLength</span></span> |<span data-ttu-id="1da34-342">相異使用者 hello 熱門項目數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="1da34-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="1da34-343">MaxUserLength</span></span> |<span data-ttu-id="1da34-344">使用者之不同項目的最大數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="1da34-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="1da34-345">MinItemLength</span></span> |<span data-ttu-id="1da34-346">項目之不同使用者的最大數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="1da34-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="1da34-347">MinUserLength</span></span> |<span data-ttu-id="1da34-348">使用者之不同項目的最小數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="1da34-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="1da34-349">RawNumberOfItems</span></span> |<span data-ttu-id="1da34-350">Hello 使用量檔案中的項目數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="1da34-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="1da34-351">RawNumberOfUsers</span></span> |<span data-ttu-id="1da34-352">任何剪除動作之前的使用點數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="1da34-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="1da34-353">RawNumberOfRecords</span></span> |<span data-ttu-id="1da34-354">任何剪除動作之前的使用點數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="1da34-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="1da34-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="1da34-356">N/A</span><span class="sxs-lookup"><span data-stu-id="1da34-356">N/A</span></span> |
| <span data-ttu-id="1da34-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="1da34-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="1da34-358">N/A</span><span class="sxs-lookup"><span data-stu-id="1da34-358">N/A</span></span> |
| <span data-ttu-id="1da34-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="1da34-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="1da34-360">N/A</span><span class="sxs-lookup"><span data-stu-id="1da34-360">N/A</span></span> |

<span data-ttu-id="1da34-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-361">OData XML</span></span>

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

### <a name="62----model-insight"></a><span data-ttu-id="1da34-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-362">6.2.</span></span>    <span data-ttu-id="1da34-363">模型深入了解</span><span class="sxs-lookup"><span data-stu-id="1da34-363">Model Insight</span></span>
<span data-ttu-id="1da34-364">傳回的深入了解模型 hello active 組建 （如果有） 或在特定的組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="1da34-365">僅適用於建議組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="1da34-366">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-366">HTTP Method</span></span> | <span data-ttu-id="1da34-367">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-368">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-368">GET</span></span> |<span data-ttu-id="1da34-369">具有作用中組建識別碼：</span><span class="sxs-lookup"><span data-stu-id="1da34-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-370">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-371">具有特定組建識別碼：</span><span class="sxs-lookup"><span data-stu-id="1da34-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-372">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-372">Parameter Name</span></span> | <span data-ttu-id="1da34-373">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-374">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-374">modelId</span></span> |<span data-ttu-id="1da34-375">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-376">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-376">buildId</span></span> |<span data-ttu-id="1da34-377">選擇性 – 識別成功組建的編號。</span><span class="sxs-lookup"><span data-stu-id="1da34-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="1da34-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-378">apiVersion</span></span> |<span data-ttu-id="1da34-379">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-379">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-380">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-380">Request Body</span></span> |<span data-ttu-id="1da34-381">無</span><span class="sxs-lookup"><span data-stu-id="1da34-381">NONE</span></span> |

<span data-ttu-id="1da34-382">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-382">**Response**:</span></span>

<span data-ttu-id="1da34-383">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-383">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-384">hello 資料是以屬性的集合傳回。</span><span class="sxs-lookup"><span data-stu-id="1da34-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="1da34-385">hello 下表描述每個索引鍵所代表的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="1da34-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="1da34-386">Key</span><span class="sxs-lookup"><span data-stu-id="1da34-386">Key</span></span> | <span data-ttu-id="1da34-387">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="1da34-388">CatalogCoverage</span></span> |<span data-ttu-id="1da34-389">Hello 類別目錄的哪個部分可以與使用模式和模型化。</span><span class="sxs-lookup"><span data-stu-id="1da34-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="1da34-390">hello rest 的 hello 項目必須以內容為基礎的功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="1da34-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="1da34-391">Mpr</span></span> |<span data-ttu-id="1da34-392">表示 hello 模型的百分位數等級。</span><span class="sxs-lookup"><span data-stu-id="1da34-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="1da34-393">越低越好。</span><span class="sxs-lookup"><span data-stu-id="1da34-393">Lower is better.</span></span> |
| <span data-ttu-id="1da34-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="1da34-394">NumberOfDimensions</span></span> |<span data-ttu-id="1da34-395">Hello 矩陣 factorization 演算法使用的維度數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="1da34-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-396">OData XML</span></span>

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

### <a name="63----get-model-sample"></a><span data-ttu-id="1da34-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-397">6.3.</span></span>    <span data-ttu-id="1da34-398">取得模型範例</span><span class="sxs-lookup"><span data-stu-id="1da34-398">Get Model Sample</span></span>
<span data-ttu-id="1da34-399">取得 hello 建議模型的範例。</span><span class="sxs-lookup"><span data-stu-id="1da34-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="1da34-400">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-400">HTTP Method</span></span> | <span data-ttu-id="1da34-401">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-402">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="1da34-403">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-404">具有特定組建識別碼：</span><span class="sxs-lookup"><span data-stu-id="1da34-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="1da34-405">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-406">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-406">Parameter Name</span></span> | <span data-ttu-id="1da34-407">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-408">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-408">modelId</span></span> |<span data-ttu-id="1da34-409">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-410">apiVersion</span></span> |<span data-ttu-id="1da34-411">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-411">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-412">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-412">Request Body</span></span> |<span data-ttu-id="1da34-413">無</span><span class="sxs-lookup"><span data-stu-id="1da34-413">NONE</span></span> |

<span data-ttu-id="1da34-414">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-414">**Response**:</span></span>

<span data-ttu-id="1da34-415">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-415">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-416">OData XML</span></span>

<span data-ttu-id="1da34-417">以原始文字格式傳回的回應：</span><span class="sxs-lookup"><span data-stu-id="1da34-417">Response is returned in raw text format:</span></span>

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
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="1da34-418">7.模型商務規則</span><span class="sxs-lookup"><span data-stu-id="1da34-418">7. Model Business Rules</span></span>
<span data-ttu-id="1da34-419">以下是支援的規則的 hello 類型：</span><span class="sxs-lookup"><span data-stu-id="1da34-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="1da34-420"><strong>封鎖清單</strong>-封鎖清單可讓您 tooprovide 不要 tooreturn hello 建議結果中的項目清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="1da34-421"><strong>FeatureBlockList</strong> -功能封鎖清單可以讓您 tooblock 項目依據其功能 hello 值。</span><span class="sxs-lookup"><span data-stu-id="1da34-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="1da34-422">*請勿在單一封鎖清單規則中傳送超過 1000 個項目，否則您的呼叫可能會逾時。如果您需要 tooblock 超過 1000 個項目，您可以進行數次的封鎖清單呼叫。*</span><span class="sxs-lookup"><span data-stu-id="1da34-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="1da34-423"><strong>Upsale</strong> -Upsale 可讓您將項目 tooreturn tooenforce hello 建議結果中的。</span><span class="sxs-lookup"><span data-stu-id="1da34-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="1da34-424"><strong>白名單</strong>-白名單可讓您 tooonly 建議清單建議項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="1da34-425"><strong>FeatureWhiteList</strong> -功能白名單可讓您有特定的功能值 tooonly 建議項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="1da34-426"><strong>PerSeedBlockList</strong> -每次種子的區塊清單可讓您 tooprovide 每個項目不可當做建議結果傳回的項目清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="1da34-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-427">7.1.</span></span>    <span data-ttu-id="1da34-428">取得模型規則</span><span class="sxs-lookup"><span data-stu-id="1da34-428">Get Model Rules</span></span>
| <span data-ttu-id="1da34-429">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-429">HTTP Method</span></span> | <span data-ttu-id="1da34-430">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-431">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="1da34-432">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-433">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-433">Parameter Name</span></span> | <span data-ttu-id="1da34-434">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-435">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-435">modelId</span></span> |<span data-ttu-id="1da34-436">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-437">apiVersion</span></span> |<span data-ttu-id="1da34-438">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-438">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-439">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-439">Request Body</span></span> |<span data-ttu-id="1da34-440">無</span><span class="sxs-lookup"><span data-stu-id="1da34-440">NONE</span></span> |

<span data-ttu-id="1da34-441">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-441">**Response**:</span></span>

<span data-ttu-id="1da34-442">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="1da34-443">`feed/entry/content/properties/Id` - 此規則的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="1da34-444">`feed/entry/content/properties/Type`Hello 規則的類型。</span><span class="sxs-lookup"><span data-stu-id="1da34-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="1da34-445">`feed/entry/content/properties/Parameter` - 規則參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="1da34-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-446">OData XML</span></span>

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

### <a name="72----add-rule"></a><span data-ttu-id="1da34-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-447">7.2.</span></span>    <span data-ttu-id="1da34-448">新增規則</span><span class="sxs-lookup"><span data-stu-id="1da34-448">Add Rule</span></span>
| <span data-ttu-id="1da34-449">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-449">HTTP Method</span></span> | <span data-ttu-id="1da34-450">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-451">POST</span><span class="sxs-lookup"><span data-stu-id="1da34-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="1da34-452">標頭</span><span class="sxs-lookup"><span data-stu-id="1da34-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="1da34-453">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-453">Parameter Name</span></span> | <span data-ttu-id="1da34-454">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-455">apiVersion</span></span> |<span data-ttu-id="1da34-456">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-456">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-457">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-457">Request Body</span></span> | |

<span data-ttu-id="1da34-458"><ins>當商務規則的提供項目 Id，請確定 toouse hello hello 項目的外部 Id (hello hello 類別目錄檔案中所用的相同識別碼)</ins></span><span class="sxs-lookup"><span data-stu-id="1da34-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="1da34-459">
<ins>tooadd 封鎖清單規則：</ins></span><span class="sxs-lookup"><span data-stu-id="1da34-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="1da34-460"><ins>
<ins>tooadd FeatureBlockList 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="1da34-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="1da34-461"><ins>tooadd Upsale 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="1da34-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="1da34-462">
<ins>tooadd 白名單規則：</ins></span><span class="sxs-lookup"><span data-stu-id="1da34-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="1da34-463"><ins>
<ins>tooadd FeatureWhiteList 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="1da34-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="1da34-464"><ins>tooadd PerSeedBlockList 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="1da34-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="1da34-465">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-465">**Response**:</span></span>

<span data-ttu-id="1da34-466">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-466">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-467">hello API 傳回 hello 新建立規則，其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="1da34-468">可以從下列路徑的 hello 擷取 hello 規則屬性：</span><span class="sxs-lookup"><span data-stu-id="1da34-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="1da34-469">`feed/entry/content/properties/Id` - 此規則的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="1da34-470">`feed/entry/content/properties/Type`Hello 規則的類型： 封鎖清單或 Upsale。</span><span class="sxs-lookup"><span data-stu-id="1da34-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="1da34-471">`feed/entry/content/properties/Parameter` - 規則參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="1da34-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-472">OData XML</span></span>

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

### <a name="73----delete-rule"></a><span data-ttu-id="1da34-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-473">7.3.</span></span>    <span data-ttu-id="1da34-474">刪除規則</span><span class="sxs-lookup"><span data-stu-id="1da34-474">Delete Rule</span></span>
| <span data-ttu-id="1da34-475">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-475">HTTP Method</span></span> | <span data-ttu-id="1da34-476">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-477">刪除</span><span class="sxs-lookup"><span data-stu-id="1da34-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-478">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-479">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-479">Parameter Name</span></span> | <span data-ttu-id="1da34-480">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-481">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-481">modelId</span></span> |<span data-ttu-id="1da34-482">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-483">filterId</span><span class="sxs-lookup"><span data-stu-id="1da34-483">filterId</span></span> |<span data-ttu-id="1da34-484">Hello 篩選器的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="1da34-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-485">apiVersion</span></span> |<span data-ttu-id="1da34-486">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-486">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-487">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-487">Request Body</span></span> |<span data-ttu-id="1da34-488">無</span><span class="sxs-lookup"><span data-stu-id="1da34-488">NONE</span></span> |

<span data-ttu-id="1da34-489">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-489">**Response**:</span></span>

<span data-ttu-id="1da34-490">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="1da34-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="1da34-491">7.4.</span></span>    <span data-ttu-id="1da34-492">刪除所有規則</span><span class="sxs-lookup"><span data-stu-id="1da34-492">Delete All Rules</span></span>
| <span data-ttu-id="1da34-493">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-493">HTTP Method</span></span> | <span data-ttu-id="1da34-494">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-495">刪除</span><span class="sxs-lookup"><span data-stu-id="1da34-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-496">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-497">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-497">Parameter Name</span></span> | <span data-ttu-id="1da34-498">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-499">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-499">modelId</span></span> |<span data-ttu-id="1da34-500">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-501">apiVersion</span></span> |<span data-ttu-id="1da34-502">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-502">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-503">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-503">Request Body</span></span> |<span data-ttu-id="1da34-504">無</span><span class="sxs-lookup"><span data-stu-id="1da34-504">NONE</span></span> |

<span data-ttu-id="1da34-505">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-505">**Response**:</span></span>

<span data-ttu-id="1da34-506">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="1da34-507">8.目錄</span><span class="sxs-lookup"><span data-stu-id="1da34-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="1da34-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-508">8.1.</span></span>    <span data-ttu-id="1da34-509">匯入目錄資料</span><span class="sxs-lookup"><span data-stu-id="1da34-509">Import Catalog Data</span></span>
<span data-ttu-id="1da34-510">如果您上傳數個類別目錄檔案 toohello 相同模型的數次呼叫時，我們將會插入只有 hello 新目錄項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="1da34-511">現有的項目仍會與 hello 原始值。</span><span class="sxs-lookup"><span data-stu-id="1da34-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="1da34-512">您無法使用這個方法更新目錄資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="1da34-513">hello 目錄資料應該遵循下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="1da34-514">沒有功能 - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="1da34-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="1da34-515">具有功能 - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="1da34-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="1da34-516">注意： hello 檔案大小上限為 200 MB。</span><span class="sxs-lookup"><span data-stu-id="1da34-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="1da34-517">** 格式詳細資料 **</span><span class="sxs-lookup"><span data-stu-id="1da34-517">** Format details **</span></span>

| <span data-ttu-id="1da34-518">名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-518">Name</span></span> | <span data-ttu-id="1da34-519">強制</span><span class="sxs-lookup"><span data-stu-id="1da34-519">Mandatory</span></span> | <span data-ttu-id="1da34-520">類型</span><span class="sxs-lookup"><span data-stu-id="1da34-520">Type</span></span> | <span data-ttu-id="1da34-521">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1da34-522">項目識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-522">Item Id</span></span> |<span data-ttu-id="1da34-523">是</span><span class="sxs-lookup"><span data-stu-id="1da34-523">Yes</span></span> |<span data-ttu-id="1da34-524">[A-z]、[a-z]、[0-9]、[_] &#40;底線&#41;、[-] &#40;虛線&#41;</span><span class="sxs-lookup"><span data-stu-id="1da34-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="1da34-525"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="1da34-525">Max length: 50</span></span> |<span data-ttu-id="1da34-526">項目的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="1da34-527">項目名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-527">Item Name</span></span> |<span data-ttu-id="1da34-528">是</span><span class="sxs-lookup"><span data-stu-id="1da34-528">Yes</span></span> |<span data-ttu-id="1da34-529">任何英數字元</span><span class="sxs-lookup"><span data-stu-id="1da34-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="1da34-530"> 最大長度：255</span><span class="sxs-lookup"><span data-stu-id="1da34-530">Max length: 255</span></span> |<span data-ttu-id="1da34-531">項目名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-531">Item name.</span></span> |
| <span data-ttu-id="1da34-532">項目類別</span><span class="sxs-lookup"><span data-stu-id="1da34-532">Item Category</span></span> |<span data-ttu-id="1da34-533">是</span><span class="sxs-lookup"><span data-stu-id="1da34-533">Yes</span></span> |<span data-ttu-id="1da34-534">任何英數字元</span><span class="sxs-lookup"><span data-stu-id="1da34-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="1da34-535"> 最大長度：255</span><span class="sxs-lookup"><span data-stu-id="1da34-535">Max length: 255</span></span> |<span data-ttu-id="1da34-536">類別 toowhich 此項目所屬 （例如烹飪的書籍，戲劇...）。可以是空的。</span><span class="sxs-lookup"><span data-stu-id="1da34-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="1da34-537">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-537">Description</span></span> |<span data-ttu-id="1da34-538">否，除非顯示功能 (但可能是空的)</span><span class="sxs-lookup"><span data-stu-id="1da34-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="1da34-539">任何英數字元</span><span class="sxs-lookup"><span data-stu-id="1da34-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="1da34-540"> 最大長度：4000</span><span class="sxs-lookup"><span data-stu-id="1da34-540">Max length: 4000</span></span> |<span data-ttu-id="1da34-541">此項目的說明。</span><span class="sxs-lookup"><span data-stu-id="1da34-541">Description of this item.</span></span> |
| <span data-ttu-id="1da34-542">功能清單</span><span class="sxs-lookup"><span data-stu-id="1da34-542">Features list</span></span> |<span data-ttu-id="1da34-543">否</span><span class="sxs-lookup"><span data-stu-id="1da34-543">No</span></span> |<span data-ttu-id="1da34-544">任何英數字元</span><span class="sxs-lookup"><span data-stu-id="1da34-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="1da34-545"> 最大長度：4000；功能數目上限：20</span><span class="sxs-lookup"><span data-stu-id="1da34-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="1da34-546">以逗號分隔清單的功能名稱 = 功能值，可以是使用的 tooenhance 模型建議。請參閱[進階主題](#2-advanced-topics)> 一節。</span><span class="sxs-lookup"><span data-stu-id="1da34-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="1da34-547">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-547">HTTP Method</span></span> | <span data-ttu-id="1da34-548">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-549">POST</span><span class="sxs-lookup"><span data-stu-id="1da34-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-550">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="1da34-551">標頭</span><span class="sxs-lookup"><span data-stu-id="1da34-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="1da34-552">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-552">Parameter Name</span></span> | <span data-ttu-id="1da34-553">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-554">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-554">modelId</span></span> |<span data-ttu-id="1da34-555">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-556">檔名</span><span class="sxs-lookup"><span data-stu-id="1da34-556">filename</span></span> |<span data-ttu-id="1da34-557">文字 hello 目錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="1da34-558">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="1da34-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="1da34-559"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="1da34-559">Max length: 50</span></span> |
| <span data-ttu-id="1da34-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-560">apiVersion</span></span> |<span data-ttu-id="1da34-561">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-561">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-562">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-562">Request Body</span></span> |<span data-ttu-id="1da34-563">範例 (包含功能)：</span><span class="sxs-lookup"><span data-stu-id="1da34-563">Example (with features):</span></span><br/><span data-ttu-id="1da34-564">2406e770-769 c-4189-89de-1c9283f93a96，亞克拉拉 Callan，活頁簿，hello 活頁簿描述，撰寫 = Richard Wright 發行者 = Harper Flamingo 加拿大，年 = 2001年</span><span class="sxs-lookup"><span data-stu-id="1da34-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="1da34-565">21bf8088-b6c0-4509-870 c-e1c7ac78304a，hello Forgetting 聊天室： 小說 （拜占庭活頁簿）、 書籍、 撰寫 = Nick Bantock 發行者 = Harpercollins，年 = 1997年</span><span class="sxs-lookup"><span data-stu-id="1da34-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="1da34-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="1da34-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="1da34-567">552a1940-21e4-4399-82bb-594b46d7ed54，我們必須把這些本例中，活頁簿，hello 活頁簿描述，撰寫 = Magnus 廠發行者 = 遊樂場發行年 = 1998年</span><span class="sxs-lookup"><span data-stu-id="1da34-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="1da34-568">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-568">**Response**:</span></span>

<span data-ttu-id="1da34-569">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-569">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-570">hello API 傳回的 hello 匯入的報表。</span><span class="sxs-lookup"><span data-stu-id="1da34-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="1da34-571">`feed\entry\content\properties\LineCount` - 已接受的行數。</span><span class="sxs-lookup"><span data-stu-id="1da34-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="1da34-572">`feed\entry\content\properties\ErrorCount`-不因為 tooan 錯誤插入的行數。</span><span class="sxs-lookup"><span data-stu-id="1da34-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="1da34-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-573">OData XML</span></span>

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

### <a name="82----get-catalog"></a><span data-ttu-id="1da34-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-574">8.2.</span></span>    <span data-ttu-id="1da34-575">取得目錄</span><span class="sxs-lookup"><span data-stu-id="1da34-575">Get Catalog</span></span>
<span data-ttu-id="1da34-576">擷取所有目錄項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="1da34-577">hello 目錄是一次擷取一個頁面。</span><span class="sxs-lookup"><span data-stu-id="1da34-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="1da34-578">如果您想 tooget 特定索引處的項目，您可以使用 hello $skip odata 參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="1da34-579">執行個體要 tooget 項目從 100 的位置開始，如果加入 hello 參數 $skip = 100 toohello 要求。</span><span class="sxs-lookup"><span data-stu-id="1da34-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="1da34-580">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-580">HTTP Method</span></span> | <span data-ttu-id="1da34-581">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-582">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-583">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-584">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-584">Parameter Name</span></span> | <span data-ttu-id="1da34-585">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-586">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-586">modelId</span></span> |<span data-ttu-id="1da34-587">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-588">apiVersion</span></span> |<span data-ttu-id="1da34-589">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-589">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-590">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-590">Request Body</span></span> |<span data-ttu-id="1da34-591">無</span><span class="sxs-lookup"><span data-stu-id="1da34-591">NONE</span></span> |

<span data-ttu-id="1da34-592">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-592">**Response**:</span></span>

<span data-ttu-id="1da34-593">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-593">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-594">hello 回應包含一個項目，每個類別目錄項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="1da34-595">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-596">`feed/entry/content/properties/ExternalId`為目錄項目外部 ID、 hello hello 客戶所提供的其中一個。</span><span class="sxs-lookup"><span data-stu-id="1da34-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="1da34-597">`feed/entry/content/properties/InternalId`類別目錄項目內部識別碼 hello Azure 機器學習建議已產生的其中一個。</span><span class="sxs-lookup"><span data-stu-id="1da34-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="1da34-598">`feed/entry/content/properties/Name` - 目錄項目名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="1da34-599">`feed/entry/content/properties/Category` - 目錄項目類別。</span><span class="sxs-lookup"><span data-stu-id="1da34-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="1da34-600">`feed/entry/content/properties/Description` - 目錄項目說明。</span><span class="sxs-lookup"><span data-stu-id="1da34-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="1da34-601">`feed/entry/content/properties/Metadata` - 目錄項目中繼資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="1da34-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-602">OData XML</span></span>

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
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="1da34-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-603">8.3.</span></span>    <span data-ttu-id="1da34-604">依語彙基元取得目錄項目</span><span class="sxs-lookup"><span data-stu-id="1da34-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="1da34-605">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-605">HTTP Method</span></span> | <span data-ttu-id="1da34-606">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-607">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-608">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-609">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-609">Parameter Name</span></span> | <span data-ttu-id="1da34-610">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-611">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-611">modelId</span></span> |<span data-ttu-id="1da34-612">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-613">token</span><span class="sxs-lookup"><span data-stu-id="1da34-613">token</span></span> |<span data-ttu-id="1da34-614">語彙基元的 hello 類別目錄項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="1da34-615">應該至少包含 3 個字元。</span><span class="sxs-lookup"><span data-stu-id="1da34-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="1da34-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-616">apiVersion</span></span> |<span data-ttu-id="1da34-617">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-617">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-618">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-618">Request Body</span></span> |<span data-ttu-id="1da34-619">無</span><span class="sxs-lookup"><span data-stu-id="1da34-619">NONE</span></span> |

<span data-ttu-id="1da34-620">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-620">**Response**:</span></span>

<span data-ttu-id="1da34-621">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-621">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-622">hello 回應包含一個項目，每個類別目錄項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="1da34-623">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-624">`feed/entry/content/properties/InternalId`類別目錄項目內部識別碼 hello Azure 機器學習建議已產生的其中一個。</span><span class="sxs-lookup"><span data-stu-id="1da34-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="1da34-625">`feed/entry/content/properties/Name` - 目錄項目名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="1da34-626">`feed/entry/content/properties/Rating` - (保留供日後使用)</span><span class="sxs-lookup"><span data-stu-id="1da34-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="1da34-627">`feed/entry/content/properties/Reasoning` - (保留供日後使用)</span><span class="sxs-lookup"><span data-stu-id="1da34-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="1da34-628">`feed/entry/content/properties/Metadata` - (保留供日後使用)</span><span class="sxs-lookup"><span data-stu-id="1da34-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="1da34-629">`feed/entry/content/properties/FormattedRating` - (保留供日後使用)</span><span class="sxs-lookup"><span data-stu-id="1da34-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="1da34-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-630">OData XML</span></span>

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

## <a name="9-usage-data"></a><span data-ttu-id="1da34-631">9.使用狀況資料</span><span class="sxs-lookup"><span data-stu-id="1da34-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="1da34-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-632">9.1.</span></span>    <span data-ttu-id="1da34-633">匯入使用資料</span><span class="sxs-lookup"><span data-stu-id="1da34-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="1da34-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-634">9.1.1.</span></span> <span data-ttu-id="1da34-635">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="1da34-635">Uploading File</span></span>
<span data-ttu-id="1da34-636">本節說明如何使用檔案 tooupload 使用量資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="1da34-637">您可以利用使用資料呼叫此 API 數次。</span><span class="sxs-lookup"><span data-stu-id="1da34-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="1da34-638">將會針對所有呼叫儲存所有使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="1da34-639">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-639">HTTP Method</span></span> | <span data-ttu-id="1da34-640">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-641">POST</span><span class="sxs-lookup"><span data-stu-id="1da34-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-642">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-643">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-643">Parameter Name</span></span> | <span data-ttu-id="1da34-644">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-645">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-645">modelId</span></span> |<span data-ttu-id="1da34-646">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-647">檔名</span><span class="sxs-lookup"><span data-stu-id="1da34-647">filename</span></span> |<span data-ttu-id="1da34-648">文字 hello 目錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="1da34-649">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="1da34-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="1da34-650"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="1da34-650">Max length: 50</span></span> |
| <span data-ttu-id="1da34-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-651">apiVersion</span></span> |<span data-ttu-id="1da34-652">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-652">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-653">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-653">Request Body</span></span> |<span data-ttu-id="1da34-654">使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-654">Usage data.</span></span> <span data-ttu-id="1da34-655">格式：</span><span class="sxs-lookup"><span data-stu-id="1da34-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="1da34-656">名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-656">Name</span></span></th><th><span data-ttu-id="1da34-657">強制</span><span class="sxs-lookup"><span data-stu-id="1da34-657">Mandatory</span></span></th><th><span data-ttu-id="1da34-658">類型</span><span class="sxs-lookup"><span data-stu-id="1da34-658">Type</span></span></th><th><span data-ttu-id="1da34-659">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-659">Description</span></span></th></tr><tr><td><span data-ttu-id="1da34-660">使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-660">User Id</span></span></td><td><span data-ttu-id="1da34-661">yes</span><span class="sxs-lookup"><span data-stu-id="1da34-661">Yes</span></span></td><td><span data-ttu-id="1da34-662">[A-z]、[a-z]、[0-9]、[_] &#40;底線&#41;、[-] &#40;虛線&#41;</span><span class="sxs-lookup"><span data-stu-id="1da34-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="1da34-663"> 最大長度：255</span><span class="sxs-lookup"><span data-stu-id="1da34-663">Max length: 255</span></span> </td><td><span data-ttu-id="1da34-664">使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="1da34-665">項目識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-665">Item Id</span></span></td><td><span data-ttu-id="1da34-666">是</span><span class="sxs-lookup"><span data-stu-id="1da34-666">Yes</span></span></td><td><span data-ttu-id="1da34-667">[A-z]、[a-z]、[0-9]、[&#95;] &#40;底線&#41;、[-] &#40;虛線&#41;</span><span class="sxs-lookup"><span data-stu-id="1da34-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="1da34-668"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="1da34-668">Max length: 50</span></span></td><td><span data-ttu-id="1da34-669">項目的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="1da34-670">時間</span><span class="sxs-lookup"><span data-stu-id="1da34-670">Time</span></span></td><td><span data-ttu-id="1da34-671">否</span><span class="sxs-lookup"><span data-stu-id="1da34-671">No</span></span></td><td><span data-ttu-id="1da34-672">日期格式：YYYY/MM/DDTHH:MM:SS (例如 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="1da34-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="1da34-673">資料的時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="1da34-674">事件</span><span class="sxs-lookup"><span data-stu-id="1da34-674">Event</span></span></td><td><span data-ttu-id="1da34-675">否；如果提供，必須也提供日期</span><span class="sxs-lookup"><span data-stu-id="1da34-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="1da34-676">下列其中一種 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-676">One of hello following:</span></span><br><span data-ttu-id="1da34-677">• Click</span><span class="sxs-lookup"><span data-stu-id="1da34-677">• Click</span></span><br><span data-ttu-id="1da34-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="1da34-678">• RecommendationClick</span></span><br><span data-ttu-id="1da34-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="1da34-679">•    AddShopCart</span></span><br><span data-ttu-id="1da34-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="1da34-680">• RemoveShopCart</span></span><br><span data-ttu-id="1da34-681">• 購買</span><span class="sxs-lookup"><span data-stu-id="1da34-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="1da34-682">檔案大小上限：200MB</span><span class="sxs-lookup"><span data-stu-id="1da34-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="1da34-683">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="1da34-684">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-684">**Response**:</span></span>

<span data-ttu-id="1da34-685">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="1da34-686">`Feed\entry\content\properties\LineCount` - 已接受的行數。</span><span class="sxs-lookup"><span data-stu-id="1da34-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="1da34-687">`Feed\entry\content\properties\ErrorCount`-不因為 tooan 錯誤插入的行數。</span><span class="sxs-lookup"><span data-stu-id="1da34-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="1da34-688">`Feed\entry\content\properties\FileId` - 檔案識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="1da34-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-689">OData XML</span></span>

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


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="1da34-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-690">9.1.2.</span></span> <span data-ttu-id="1da34-691">使用資料擷取</span><span class="sxs-lookup"><span data-stu-id="1da34-691">Using Data Acquisition</span></span>
<span data-ttu-id="1da34-692">本節說明如何在真實 toosend 事件時間 tooAzure 機器學習的建議事項，通常是從您的網站。</span><span class="sxs-lookup"><span data-stu-id="1da34-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="1da34-693">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-693">HTTP Method</span></span> | <span data-ttu-id="1da34-694">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-695">POST</span><span class="sxs-lookup"><span data-stu-id="1da34-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="1da34-696">標頭</span><span class="sxs-lookup"><span data-stu-id="1da34-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="1da34-697">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-697">Parameter Name</span></span> | <span data-ttu-id="1da34-698">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-699">apiVersion</span></span> |<span data-ttu-id="1da34-700">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-700">1.0</span></span> |
| <span data-ttu-id="1da34-701">Request body</span><span class="sxs-lookup"><span data-stu-id="1da34-701">Request body</span></span> |<span data-ttu-id="1da34-702">事件資料輸入您要為每個事件 toosend。</span><span class="sxs-lookup"><span data-stu-id="1da34-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="1da34-703">您應該傳送的 hello 相同的使用者或瀏覽器工作階段 hello hello SessionId 欄位中的相同識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="1da34-704">(請參閱下面的事件本文範例。)</span><span class="sxs-lookup"><span data-stu-id="1da34-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="1da34-705">事件 'Click' 的範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="1da34-706">事件 'RecommendationClick' 的範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="1da34-707">事件 'AddShopCart' 的範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="1da34-708">事件 'RemoveShopCart' 的範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="1da34-709">事件 'Purchase' 的範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-709">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="1da34-710">傳送 2 個事件 ('Click' 和 'AddShopCart') 的範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="1da34-711">**回應**：HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="1da34-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-712">9.2.</span></span>    <span data-ttu-id="1da34-713">列出模型使用方式檔案</span><span class="sxs-lookup"><span data-stu-id="1da34-713">List Model Usage Files</span></span>
<span data-ttu-id="1da34-714">擷取所有模型使用方式檔案的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="1da34-715">hello 使用量檔案會擷取一頁一次。</span><span class="sxs-lookup"><span data-stu-id="1da34-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="1da34-716">每個頁面包含 100 個項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-716">Each page containes 100 items.</span></span> <span data-ttu-id="1da34-717">如果您想 tooget 特定索引處的項目，您可以使用 hello $skip odata 參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="1da34-718">執行個體要 tooget 項目從 100 的位置開始，如果加入 hello 參數 $skip = 100 toohello 要求。</span><span class="sxs-lookup"><span data-stu-id="1da34-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="1da34-719">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-719">HTTP Method</span></span> | <span data-ttu-id="1da34-720">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-721">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-722">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-723">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-723">Parameter Name</span></span> | <span data-ttu-id="1da34-724">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="1da34-725">forModelId</span></span> |<span data-ttu-id="1da34-726">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-727">apiVersion</span></span> |<span data-ttu-id="1da34-728">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-728">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-729">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-729">Request Body</span></span> |<span data-ttu-id="1da34-730">無</span><span class="sxs-lookup"><span data-stu-id="1da34-730">NONE</span></span> |

<span data-ttu-id="1da34-731">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-731">**Response**:</span></span>

<span data-ttu-id="1da34-732">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-732">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-733">hello 回應會包含每個使用量檔案的一個項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="1da34-734">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-735">`feed\entry\content\properties\Id` - 使用狀況檔案識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="1da34-736">`feed\entry\content\properties\Length` - 使用狀況檔案長度，以 MB 為單位。</span><span class="sxs-lookup"><span data-stu-id="1da34-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="1da34-737">`feed\entry\content\properties\DateModified`-建立 hello 使用量檔案的日期。</span><span class="sxs-lookup"><span data-stu-id="1da34-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="1da34-738">`feed\entry\content\properties\UseInModel`-是否 hello 使用量檔案 hello 模型中使用。</span><span class="sxs-lookup"><span data-stu-id="1da34-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="1da34-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-739">OData XML</span></span>

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

### <a name="93----get-usage-statistics"></a><span data-ttu-id="1da34-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-740">9.3.</span></span>    <span data-ttu-id="1da34-741">取得使用狀況統計資料</span><span class="sxs-lookup"><span data-stu-id="1da34-741">Get Usage Statistics</span></span>
<span data-ttu-id="1da34-742">取得使用狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-742">Gets usage statistics.</span></span>

| <span data-ttu-id="1da34-743">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-743">HTTP Method</span></span> | <span data-ttu-id="1da34-744">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-745">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-746">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-747">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-747">Parameter Name</span></span> | <span data-ttu-id="1da34-748">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-749">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-749">modelId</span></span> |<span data-ttu-id="1da34-750">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-751">startDate</span><span class="sxs-lookup"><span data-stu-id="1da34-751">startDate</span></span> |<span data-ttu-id="1da34-752">開始日期。</span><span class="sxs-lookup"><span data-stu-id="1da34-752">Start date.</span></span> <span data-ttu-id="1da34-753">格式：yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="1da34-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="1da34-754">endDate</span><span class="sxs-lookup"><span data-stu-id="1da34-754">endDate</span></span> |<span data-ttu-id="1da34-755">結束日期。</span><span class="sxs-lookup"><span data-stu-id="1da34-755">End date.</span></span> <span data-ttu-id="1da34-756">格式：yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="1da34-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="1da34-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="1da34-757">eventTypes</span></span> |<span data-ttu-id="1da34-758">以逗號分隔字串的事件類型或 null tooget 所有事件</span><span class="sxs-lookup"><span data-stu-id="1da34-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="1da34-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-759">apiVersion</span></span> |<span data-ttu-id="1da34-760">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-760">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-761">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-761">Request Body</span></span> |<span data-ttu-id="1da34-762">無</span><span class="sxs-lookup"><span data-stu-id="1da34-762">NONE</span></span> |

<span data-ttu-id="1da34-763">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-763">**Response**:</span></span>

<span data-ttu-id="1da34-764">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-764">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-765">索引鍵/值項目的集合。</span><span class="sxs-lookup"><span data-stu-id="1da34-765">A collection of key/value elements.</span></span> <span data-ttu-id="1da34-766">每個包含 hello 總和的每小時分組特定事件類型的事件。</span><span class="sxs-lookup"><span data-stu-id="1da34-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="1da34-767">`feed\entry[i]\content\properties\Key`-包含 （依小時分組） 的 hello 時間與 hello 事件類型。</span><span class="sxs-lookup"><span data-stu-id="1da34-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="1da34-768">`feed\entry[i]\content\properties\Value` - 事件總數。</span><span class="sxs-lookup"><span data-stu-id="1da34-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="1da34-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-769">OData XML</span></span>

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

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="1da34-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="1da34-770">9.4.</span></span>    <span data-ttu-id="1da34-771">取得使用方式檔案範例</span><span class="sxs-lookup"><span data-stu-id="1da34-771">Get Usage File Sample</span></span>
<span data-ttu-id="1da34-772">擷取 hello 的使用方式檔案內容的第一個 2 KB。</span><span class="sxs-lookup"><span data-stu-id="1da34-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="1da34-773">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-773">HTTP Method</span></span> | <span data-ttu-id="1da34-774">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-775">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-776">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-777">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-777">Parameter Name</span></span> | <span data-ttu-id="1da34-778">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-779">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-779">modelId</span></span> |<span data-ttu-id="1da34-780">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-781">fileId</span><span class="sxs-lookup"><span data-stu-id="1da34-781">fileId</span></span> |<span data-ttu-id="1da34-782">Hello 模型使用方式檔案的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="1da34-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-783">apiVersion</span></span> |<span data-ttu-id="1da34-784">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-784">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-785">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-785">Request Body</span></span> |<span data-ttu-id="1da34-786">無</span><span class="sxs-lookup"><span data-stu-id="1da34-786">NONE</span></span> |

<span data-ttu-id="1da34-787">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-787">**Response**:</span></span>

<span data-ttu-id="1da34-788">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-788">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-789">以原始文字格式傳回的回應：</span><span class="sxs-lookup"><span data-stu-id="1da34-789">Response is returned in raw text format:</span></span>

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


### <a name="95----get-model-usage-file"></a><span data-ttu-id="1da34-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="1da34-790">9.5.</span></span>    <span data-ttu-id="1da34-791">取得模型使用方式檔案</span><span class="sxs-lookup"><span data-stu-id="1da34-791">Get Model Usage File</span></span>
<span data-ttu-id="1da34-792">擷取 hello 的 hello 使用量檔案的完整內容。</span><span class="sxs-lookup"><span data-stu-id="1da34-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="1da34-793">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-793">HTTP Method</span></span> | <span data-ttu-id="1da34-794">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-795">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-796">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-797">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-797">Parameter Name</span></span> | <span data-ttu-id="1da34-798">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-799">mid</span><span class="sxs-lookup"><span data-stu-id="1da34-799">mid</span></span> |<span data-ttu-id="1da34-800">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-801">fid</span><span class="sxs-lookup"><span data-stu-id="1da34-801">fid</span></span> |<span data-ttu-id="1da34-802">Hello 模型使用方式檔案的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="1da34-803">下載</span><span class="sxs-lookup"><span data-stu-id="1da34-803">download</span></span> |<span data-ttu-id="1da34-804">1</span><span class="sxs-lookup"><span data-stu-id="1da34-804">1</span></span> |
| <span data-ttu-id="1da34-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-805">apiVersion</span></span> |<span data-ttu-id="1da34-806">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-806">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-807">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-807">Request Body</span></span> |<span data-ttu-id="1da34-808">無</span><span class="sxs-lookup"><span data-stu-id="1da34-808">NONE</span></span> |

<span data-ttu-id="1da34-809">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-809">**Response**:</span></span>

<span data-ttu-id="1da34-810">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-810">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-811">以原始文字格式傳回的回應：</span><span class="sxs-lookup"><span data-stu-id="1da34-811">Response is returned in raw text format:</span></span>

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

### <a name="96----delete-usage-file"></a><span data-ttu-id="1da34-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="1da34-812">9.6.</span></span>    <span data-ttu-id="1da34-813">刪除使用方式檔案</span><span class="sxs-lookup"><span data-stu-id="1da34-813">Delete Usage File</span></span>
<span data-ttu-id="1da34-814">刪除 hello 指定的模型使用方式檔案。</span><span class="sxs-lookup"><span data-stu-id="1da34-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="1da34-815">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-815">HTTP Method</span></span> | <span data-ttu-id="1da34-816">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-817">刪除</span><span class="sxs-lookup"><span data-stu-id="1da34-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-818">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-819">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-819">Parameter Name</span></span> | <span data-ttu-id="1da34-820">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-821">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-821">modelId</span></span> |<span data-ttu-id="1da34-822">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-823">fileId</span><span class="sxs-lookup"><span data-stu-id="1da34-823">fileId</span></span> |<span data-ttu-id="1da34-824">刪除 hello 檔案 toobe 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="1da34-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-825">apiVersion</span></span> |<span data-ttu-id="1da34-826">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-826">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-827">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-827">Request Body</span></span> |<span data-ttu-id="1da34-828">無</span><span class="sxs-lookup"><span data-stu-id="1da34-828">NONE</span></span> |

<span data-ttu-id="1da34-829">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-829">**Response**:</span></span>

<span data-ttu-id="1da34-830">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="1da34-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="1da34-831">9.7.</span></span>    <span data-ttu-id="1da34-832">刪除所有使用方式檔案</span><span class="sxs-lookup"><span data-stu-id="1da34-832">Delete All Usage Files</span></span>
<span data-ttu-id="1da34-833">刪除所有模型使用方式檔案。</span><span class="sxs-lookup"><span data-stu-id="1da34-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="1da34-834">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-834">HTTP Method</span></span> | <span data-ttu-id="1da34-835">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-836">刪除</span><span class="sxs-lookup"><span data-stu-id="1da34-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-837">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-838">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-838">Parameter Name</span></span> | <span data-ttu-id="1da34-839">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-840">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-840">modelId</span></span> |<span data-ttu-id="1da34-841">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-842">apiVersion</span></span> |<span data-ttu-id="1da34-843">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-843">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-844">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-844">Request Body</span></span> |<span data-ttu-id="1da34-845">無</span><span class="sxs-lookup"><span data-stu-id="1da34-845">NONE</span></span> |

<span data-ttu-id="1da34-846">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-846">**Response**:</span></span>

<span data-ttu-id="1da34-847">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="1da34-848">10.特性</span><span class="sxs-lookup"><span data-stu-id="1da34-848">10. Features</span></span>
<span data-ttu-id="1da34-849">本節說明 tooretrieve 功能資訊，例如 hello 匯入功能和其值、 其等級的方式和此陣序時所配置。</span><span class="sxs-lookup"><span data-stu-id="1da34-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="1da34-850">功能以資料的一部分 hello 類別目錄，匯入且然後陣序相關聯等級的組建完成時。</span><span class="sxs-lookup"><span data-stu-id="1da34-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="1da34-851">使用量資料和項目類型的相應的 toohello 模式時，可以變更功能等級。</span><span class="sxs-lookup"><span data-stu-id="1da34-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="1da34-852">但一致使用量/項目，hello 陣序規範應該有小型的波動。</span><span class="sxs-lookup"><span data-stu-id="1da34-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="1da34-853">hello 陣序的功能為非負數。</span><span class="sxs-lookup"><span data-stu-id="1da34-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="1da34-854">hello 的數字 0 表示該 hello 功能不次序比它 （如果您叫用 hello 第一次的陣序建置此應用程式開發介面先前 toohello 完成會發生）。</span><span class="sxs-lookup"><span data-stu-id="1da34-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="1da34-855">hello 日期 hello 陣序使用的屬性稱為 hello 分數有效期限。</span><span class="sxs-lookup"><span data-stu-id="1da34-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="1da34-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-856">10.1.</span></span> <span data-ttu-id="1da34-857">取得功能資訊 (適用於上一個排名組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="1da34-858">擷取 hello 功能的資訊，包括排名 hello 最後一個成功次序組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="1da34-859">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-859">HTTP Method</span></span> | <span data-ttu-id="1da34-860">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-861">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-862">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-863">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-863">Parameter Name</span></span> | <span data-ttu-id="1da34-864">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-865">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-865">modelId</span></span> |<span data-ttu-id="1da34-866">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="1da34-867">samplingSize</span></span> |<span data-ttu-id="1da34-868">針對每個功能，根據 toohello 資料出現在 hello 類別目錄值 tooinclude 數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="1da34-869">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="1da34-869">Possible values are:</span></span><br> <span data-ttu-id="1da34-870">-1 - 所有範例。</span><span class="sxs-lookup"><span data-stu-id="1da34-870">-1 - All samples.</span></span> <br><span data-ttu-id="1da34-871">0 - 沒有取樣。</span><span class="sxs-lookup"><span data-stu-id="1da34-871">0 - No sampling.</span></span> <br><span data-ttu-id="1da34-872">N - 傳回每個功能名稱的 N 範例。</span><span class="sxs-lookup"><span data-stu-id="1da34-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="1da34-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-873">apiVersion</span></span> |<span data-ttu-id="1da34-874">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-874">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-875">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-875">Request Body</span></span> |<span data-ttu-id="1da34-876">無</span><span class="sxs-lookup"><span data-stu-id="1da34-876">NONE</span></span> |

<span data-ttu-id="1da34-877">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-877">**Response**:</span></span>

<span data-ttu-id="1da34-878">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-878">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-879">hello 回應包含功能資訊項目的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="1da34-880">每個項目包含：</span><span class="sxs-lookup"><span data-stu-id="1da34-880">Each entry contains:</span></span>

* <span data-ttu-id="1da34-881">`feed/entry/content/m:properties/d:Name` - 功能名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="1da34-882">`feed/entry/content/m:properties/d:RankUpdateDate`日期的 hello 順位時配置的 toothis 功能也稱為</span><span class="sxs-lookup"><span data-stu-id="1da34-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="1da34-883">分數有效時間功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-883">score freshness feature.</span></span> <span data-ttu-id="1da34-884">歷程記錄日期 ('0001-01-01T00:00:00') 表示未執行排名組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="1da34-885">`feed/entry/content/m:properties/d:Rank` - 功能排名 (float)。</span><span class="sxs-lookup"><span data-stu-id="1da34-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="1da34-886">排名 2.0 以上會被視為良好的功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="1da34-887">`feed/entry/content/m:properties/d:SampleValues`-逗號分隔清單的總要求 toohello 取樣大小的值。</span><span class="sxs-lookup"><span data-stu-id="1da34-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="1da34-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
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

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="1da34-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-889">10.2.</span></span> <span data-ttu-id="1da34-890">取得功能資訊 (適用於特定排名組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="1da34-891">擷取 hello 功能的資訊，包括 hello 次序特定等級的組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="1da34-892">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-892">HTTP Method</span></span> | <span data-ttu-id="1da34-893">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-894">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-895">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-896">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-896">Parameter Name</span></span> | <span data-ttu-id="1da34-897">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-898">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-898">modelId</span></span> |<span data-ttu-id="1da34-899">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="1da34-900">samplingSize</span></span> |<span data-ttu-id="1da34-901">針對每個功能，根據 toohello 資料出現在 hello 類別目錄值 tooinclude 數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="1da34-902">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="1da34-902">Possible values are:</span></span><br> <span data-ttu-id="1da34-903">-1 - 所有範例。</span><span class="sxs-lookup"><span data-stu-id="1da34-903">-1 - All samples.</span></span> <br><span data-ttu-id="1da34-904">0 - 沒有取樣。</span><span class="sxs-lookup"><span data-stu-id="1da34-904">0 - No sampling.</span></span> <br><span data-ttu-id="1da34-905">N - 傳回每個功能名稱的 N 範例。</span><span class="sxs-lookup"><span data-stu-id="1da34-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="1da34-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="1da34-906">rankBuildId</span></span> |<span data-ttu-id="1da34-907">Hello 次序組建或-1 代表 hello 最後一次的陣序組建的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="1da34-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-908">apiVersion</span></span> |<span data-ttu-id="1da34-909">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-909">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-910">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-910">Request Body</span></span> |<span data-ttu-id="1da34-911">無</span><span class="sxs-lookup"><span data-stu-id="1da34-911">NONE</span></span> |

<span data-ttu-id="1da34-912">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-912">**Response**:</span></span>

<span data-ttu-id="1da34-913">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-913">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-914">hello 回應包含功能資訊項目的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="1da34-915">每個項目包含：</span><span class="sxs-lookup"><span data-stu-id="1da34-915">Each entry contains:</span></span>

* <span data-ttu-id="1da34-916">`feed/entry/content/m:properties/d:Name` - 功能名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="1da34-917">`feed/entry/content/m:properties/d:RankUpdateDate`日期的 hello 順位時配置的 toothis 功能也稱為</span><span class="sxs-lookup"><span data-stu-id="1da34-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="1da34-918">分數有效時間功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-918">score freshness feature.</span></span> <span data-ttu-id="1da34-919">歷程記錄日期 ('0001-01-01T00:00:00') 表示未執行排名組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="1da34-920">`feed/entry/content/m:properties/d:Rank` - 功能排名 (float)。</span><span class="sxs-lookup"><span data-stu-id="1da34-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="1da34-921">排名 2.0 以上會被視為良好的功能。</span><span class="sxs-lookup"><span data-stu-id="1da34-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="1da34-922">`feed/entry/content/m:properties/d:SampleValues`-逗號分隔清單的總要求 toohello 取樣大小的值。</span><span class="sxs-lookup"><span data-stu-id="1da34-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="1da34-923">OData</span><span class="sxs-lookup"><span data-stu-id="1da34-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
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


## <a name="11-build"></a><span data-ttu-id="1da34-924">11.建置</span><span class="sxs-lookup"><span data-stu-id="1da34-924">11. Build</span></span>
  <span data-ttu-id="1da34-925">本章節將說明 hello 不同的 Api 相關 toobuilds。</span><span class="sxs-lookup"><span data-stu-id="1da34-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="1da34-926">有 3 個類型的組建：建議組建、排名組建和 FBT (通常會一起購買) 組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="1da34-927">hello 建議組建的目的是的 toogenerate 推薦模型用於預測。</span><span class="sxs-lookup"><span data-stu-id="1da34-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="1da34-928">這種組建類型的預測可分為兩種類別：</span><span class="sxs-lookup"><span data-stu-id="1da34-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="1da34-929">I2I - 又稱為</span><span class="sxs-lookup"><span data-stu-id="1da34-929">I2I - a.k.a.</span></span> <span data-ttu-id="1da34-930">項目 tooItem 建議的指定項目或清單項目的此選項將預測的項目，則可能 toobe 高度感興趣的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="1da34-931">U2I - 又稱為</span><span class="sxs-lookup"><span data-stu-id="1da34-931">U2I - a.k.a.</span></span> <span data-ttu-id="1da34-932">指定使用者識別碼 （及選擇性的項目清單） 的使用者 tooItem 建議這個選項將預測的項目，則可能 toobe hello 給定使用者 （和其其他選擇的項目） 的高度感興趣的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="1da34-933">hello U2I 建議根據 hello 的 hello toohello 時間 hello 模型所建立的使用者感興趣的項目歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="1da34-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="1da34-934">Rank 組建會技術建置，可讓您 toolearn hello 效益功能有關。</span><span class="sxs-lookup"><span data-stu-id="1da34-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="1da34-935">通常，在順序 tooget hello 最佳結果中包含功能的建議模型，您應該採取步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="1da34-936">觸發次序組建 （除非 hello 分數的功能是穩定的） 和等候，再取得 hello 特徵分數。</span><span class="sxs-lookup"><span data-stu-id="1da34-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="1da34-937">擷取由呼叫 hello hello 陣序的功能[取得功能資訊](#101-get-features-info-for-last-rank-build)應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1da34-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="1da34-938">設定下列參數的 hello 建議組建：</span><span class="sxs-lookup"><span data-stu-id="1da34-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="1da34-939">`useFeatureInModel`-設定 tooTrue。</span><span class="sxs-lookup"><span data-stu-id="1da34-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="1da34-940">`ModelingFeatureList`-設定 tooa 以逗號分隔清單的分數為 2.0 或更多的功能 （依據 toohello 陣序規範您 hello 先前步驟中所擷取）。</span><span class="sxs-lookup"><span data-stu-id="1da34-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="1da34-941">`AllowColdItemPlacement`-設定 tooTrue。</span><span class="sxs-lookup"><span data-stu-id="1da34-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="1da34-942">您可以選擇設定`EnableFeatureCorrelation`tooTrue 和`ReasoningFeatureList`toohello 想 toouse 說明 (通常是相同的功能清單使用模型或子清單中的 hello) 的功能清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="1da34-943">觸發程序 hello 建議建置以 hello 設定參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="1da34-944">注意： 如果您未設定任何參數 （例如叫用不含參數的 hello 建議建置），或不明確地停止 hello 使用量的功能 (例如`UseFeatureInModel`設定 tooFalse)，hello 系統將會設定 hello 功能相關的參數toohello 說明上述的值，以防次序組建存在。</span><span class="sxs-lookup"><span data-stu-id="1da34-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="1da34-945">在執行中的次序組建上不受限制和建議同時建置 hello 相同模型。</span><span class="sxs-lookup"><span data-stu-id="1da34-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="1da34-946">不過，您無法執行這兩個組建的 hello hello 相同模型以平行方式在相同的類型。</span><span class="sxs-lookup"><span data-stu-id="1da34-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="1da34-947">FBT (通常會一起購買) 組建也是另一種建議運算法，有時稱為「保守的」建議者，適用於本質上並不同質的目錄 (同質：書籍、電影、一些食物、流行；非同質：電腦與裝置、跨網域、高度差異)。</span><span class="sxs-lookup"><span data-stu-id="1da34-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="1da34-948">注意： 如果 hello 您上傳的使用方式檔案包含 hello 選擇性欄位 「 事件類型 」 然後 FBT 模型的 「 採購 」 事件只有適用。</span><span class="sxs-lookup"><span data-stu-id="1da34-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="1da34-949">如果沒有提供事件類型，所有事件都會視為 Purchase。</span><span class="sxs-lookup"><span data-stu-id="1da34-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="1da34-950">11.1 組建參數</span><span class="sxs-lookup"><span data-stu-id="1da34-950">11.1 Build parameters</span></span>
<span data-ttu-id="1da34-951">每個組建類型都可以透過一組參數 (如下所述) 進行設定。</span><span class="sxs-lookup"><span data-stu-id="1da34-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="1da34-952">如果您未設定 hello 參數，hello 系統將自動屬性，根據 toohello 資訊在 hello 的時間觸發組建的 toohello 參數值。</span><span class="sxs-lookup"><span data-stu-id="1da34-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="1da34-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-953">11.1.1.</span></span> <span data-ttu-id="1da34-954">使用狀況冷凝器</span><span class="sxs-lookup"><span data-stu-id="1da34-954">Usage condenser</span></span>
<span data-ttu-id="1da34-955">附帶少數使用點的使用者或項目可能包含較多雜訊而非資訊。</span><span class="sxs-lookup"><span data-stu-id="1da34-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="1da34-956">hello 系統嘗試 toopredict hello 最少的每個模型中使用的使用者/項目 toobe 使用量點。</span><span class="sxs-lookup"><span data-stu-id="1da34-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="1da34-957">這會是 hello ItemCutoffLowerBound 和 ItemCutoffUpperBound 參數項目和 hello UserCutOffLowerBound 和使用者的 UserCutoffUpperBound 參數所定義的 hello 範圍所定義的 hello 範圍內。</span><span class="sxs-lookup"><span data-stu-id="1da34-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="1da34-958">hello 冷凝器影響項目或使用者可設定至少一個對應界限 toozero hello 降至最低。</span><span class="sxs-lookup"><span data-stu-id="1da34-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="1da34-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-959">11.1.2.</span></span> <span data-ttu-id="1da34-960">排名組建參數</span><span class="sxs-lookup"><span data-stu-id="1da34-960">Rank build parameters</span></span>
<span data-ttu-id="1da34-961">hello 下表描述 hello 次序組建的組建參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="1da34-962">Key</span><span class="sxs-lookup"><span data-stu-id="1da34-962">Key</span></span> | <span data-ttu-id="1da34-963">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-963">Description</span></span> | <span data-ttu-id="1da34-964">類型</span><span class="sxs-lookup"><span data-stu-id="1da34-964">Type</span></span> | <span data-ttu-id="1da34-965">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1da34-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="1da34-966">NumberOfModelIterations</span></span> |<span data-ttu-id="1da34-967">hello 數目 hello 模型執行的反覆項目都會反映在 hello 整體計算時間和 hello 模型精確度。</span><span class="sxs-lookup"><span data-stu-id="1da34-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="1da34-968">hello hello 編號，hello 更好的精確度，您會收到，但是 hello 計算需要較久的時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="1da34-969">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-969">Integer</span></span> |<span data-ttu-id="1da34-970">10-50</span><span class="sxs-lookup"><span data-stu-id="1da34-970">10-50</span></span> |
| <span data-ttu-id="1da34-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="1da34-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="1da34-972">維度的 hello 數目相關 toohello '功能' hello 模型數目將會嘗試 toofind 資料中。</span><span class="sxs-lookup"><span data-stu-id="1da34-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="1da34-973">增加 hello 維度的數目，可讓更好，微調 hello 結果分成較小的群集。</span><span class="sxs-lookup"><span data-stu-id="1da34-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="1da34-974">但是，太多維度會防止 hello 模型尋找項目之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="1da34-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="1da34-975">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-975">Integer</span></span> |<span data-ttu-id="1da34-976">10-40</span><span class="sxs-lookup"><span data-stu-id="1da34-976">10-40</span></span> |
| <span data-ttu-id="1da34-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="1da34-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="1da34-978">定義 hello hello 冷凝器的項目下限。</span><span class="sxs-lookup"><span data-stu-id="1da34-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="1da34-979">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-979">See usage condenser above.</span></span> |<span data-ttu-id="1da34-980">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-980">Integer</span></span> |<span data-ttu-id="1da34-981">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="1da34-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="1da34-983">定義 hello hello 冷凝器的項目上限。</span><span class="sxs-lookup"><span data-stu-id="1da34-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="1da34-984">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-984">See usage condenser above.</span></span> |<span data-ttu-id="1da34-985">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-985">Integer</span></span> |<span data-ttu-id="1da34-986">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="1da34-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="1da34-988">定義 hello 使用者下限 hello 冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="1da34-989">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-989">See usage condenser above.</span></span> |<span data-ttu-id="1da34-990">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-990">Integer</span></span> |<span data-ttu-id="1da34-991">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="1da34-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="1da34-993">定義 hello 使用者上限 hello 冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="1da34-994">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-994">See usage condenser above.</span></span> |<span data-ttu-id="1da34-995">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-995">Integer</span></span> |<span data-ttu-id="1da34-996">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="1da34-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-997">11.1.3.</span></span> <span data-ttu-id="1da34-998">建議組建參數</span><span class="sxs-lookup"><span data-stu-id="1da34-998">Recommendation build parameters</span></span>
<span data-ttu-id="1da34-999">hello 下表描述 hello 建議組建的組建參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="1da34-1000">Key</span><span class="sxs-lookup"><span data-stu-id="1da34-1000">Key</span></span> | <span data-ttu-id="1da34-1001">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-1001">Description</span></span> | <span data-ttu-id="1da34-1002">類型</span><span class="sxs-lookup"><span data-stu-id="1da34-1002">Type</span></span> | <span data-ttu-id="1da34-1003">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1da34-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="1da34-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="1da34-1005">hello 數目 hello 模型執行的反覆項目都會反映在 hello 整體計算時間和 hello 模型精確度。</span><span class="sxs-lookup"><span data-stu-id="1da34-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="1da34-1006">hello hello 編號，hello 更好的精確度，您會收到，但是 hello 計算需要較久的時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="1da34-1007">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1007">Integer</span></span> |<span data-ttu-id="1da34-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="1da34-1008">10-50</span></span> |
| <span data-ttu-id="1da34-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="1da34-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="1da34-1010">維度的 hello 數目相關 toohello '功能' hello 模型數目將會嘗試 toofind 資料中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="1da34-1011">增加 hello 維度的數目，可讓更好，微調 hello 結果分成較小的群集。</span><span class="sxs-lookup"><span data-stu-id="1da34-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="1da34-1012">但是，太多維度會防止 hello 模型尋找項目之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="1da34-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="1da34-1013">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1013">Integer</span></span> |<span data-ttu-id="1da34-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="1da34-1014">10-40</span></span> |
| <span data-ttu-id="1da34-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="1da34-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="1da34-1016">定義 hello hello 冷凝器的項目下限。</span><span class="sxs-lookup"><span data-stu-id="1da34-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="1da34-1017">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1017">See usage condenser above.</span></span> |<span data-ttu-id="1da34-1018">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1018">Integer</span></span> |<span data-ttu-id="1da34-1019">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="1da34-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="1da34-1021">定義 hello hello 冷凝器的項目上限。</span><span class="sxs-lookup"><span data-stu-id="1da34-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="1da34-1022">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1022">See usage condenser above.</span></span> |<span data-ttu-id="1da34-1023">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1023">Integer</span></span> |<span data-ttu-id="1da34-1024">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="1da34-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="1da34-1026">定義 hello 使用者下限 hello 冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="1da34-1027">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1027">See usage condenser above.</span></span> |<span data-ttu-id="1da34-1028">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1028">Integer</span></span> |<span data-ttu-id="1da34-1029">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="1da34-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="1da34-1031">定義 hello 使用者上限 hello 冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="1da34-1032">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1032">See usage condenser above.</span></span> |<span data-ttu-id="1da34-1033">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1033">Integer</span></span> |<span data-ttu-id="1da34-1034">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-1035">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-1035">Description</span></span> |<span data-ttu-id="1da34-1036">建置說明。</span><span class="sxs-lookup"><span data-stu-id="1da34-1036">Build description.</span></span> |<span data-ttu-id="1da34-1037">String</span><span class="sxs-lookup"><span data-stu-id="1da34-1037">String</span></span> |<span data-ttu-id="1da34-1038">任何文字，最多 512 個字元</span><span class="sxs-lookup"><span data-stu-id="1da34-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="1da34-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="1da34-1039">EnableModelingInsights</span></span> |<span data-ttu-id="1da34-1040">可讓您 toocompute 度量 hello 推薦模型上。</span><span class="sxs-lookup"><span data-stu-id="1da34-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="1da34-1041">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1041">Boolean</span></span> |<span data-ttu-id="1da34-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="1da34-1042">True/False</span></span> |
| <span data-ttu-id="1da34-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="1da34-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="1da34-1044">指出功能是否可以使用順序 tooenhance hello 建議模型中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="1da34-1045">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1045">Boolean</span></span> |<span data-ttu-id="1da34-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="1da34-1046">True/False</span></span> |
| <span data-ttu-id="1da34-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="1da34-1047">ModelingFeatureList</span></span> |<span data-ttu-id="1da34-1048">功能名稱 toobe 順序 tooenhance hello 建議事項中的 hello 建議組建中使用的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="1da34-1049">String</span><span class="sxs-lookup"><span data-stu-id="1da34-1049">String</span></span> |<span data-ttu-id="1da34-1050">Too512 字元組成的功能名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="1da34-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="1da34-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="1da34-1052">指出是否 hello 建議也應該推送的陌生項目透過功能相似。</span><span class="sxs-lookup"><span data-stu-id="1da34-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="1da34-1053">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1053">Boolean</span></span> |<span data-ttu-id="1da34-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="1da34-1054">True/False</span></span> |
| <span data-ttu-id="1da34-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="1da34-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="1da34-1056">指出功能是否可用於推論。</span><span class="sxs-lookup"><span data-stu-id="1da34-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="1da34-1057">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1057">Boolean</span></span> |<span data-ttu-id="1da34-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="1da34-1058">True/False</span></span> |
| <span data-ttu-id="1da34-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="1da34-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="1da34-1060">以逗號分隔清單的功能名稱 toobe 用於推理句子 （例如建議說明）。</span><span class="sxs-lookup"><span data-stu-id="1da34-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="1da34-1061">String</span><span class="sxs-lookup"><span data-stu-id="1da34-1061">String</span></span> |<span data-ttu-id="1da34-1062">Too512 字元組成的功能名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="1da34-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="1da34-1063">EnableU2I</span></span> |<span data-ttu-id="1da34-1064">也稱為允許 hello 個人化的建議</span><span class="sxs-lookup"><span data-stu-id="1da34-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="1da34-1065">U2I （使用者 tooitem 建議）。</span><span class="sxs-lookup"><span data-stu-id="1da34-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="1da34-1066">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1066">Boolean</span></span> |<span data-ttu-id="1da34-1067">True/False (預設值為 True)</span><span class="sxs-lookup"><span data-stu-id="1da34-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="1da34-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="1da34-1068">11.1.4.</span></span> <span data-ttu-id="1da34-1069">FBT 組建參數</span><span class="sxs-lookup"><span data-stu-id="1da34-1069">FBT build parameters</span></span>
<span data-ttu-id="1da34-1070">hello 下表描述 hello 建議組建的組建參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="1da34-1071">Key</span><span class="sxs-lookup"><span data-stu-id="1da34-1071">Key</span></span> | <span data-ttu-id="1da34-1072">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-1072">Description</span></span> | <span data-ttu-id="1da34-1073">類型</span><span class="sxs-lookup"><span data-stu-id="1da34-1073">Type</span></span> | <span data-ttu-id="1da34-1074">有效的值 (預設值)</span><span class="sxs-lookup"><span data-stu-id="1da34-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1da34-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="1da34-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="1da34-1076">保守 hello 模型的方式。</span><span class="sxs-lookup"><span data-stu-id="1da34-1076">How conservative hello model is.</span></span> <span data-ttu-id="1da34-1077">共同的相符項目的項目 toobe 視為模型化的數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="1da34-1078">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1078">Integer</span></span> |<span data-ttu-id="1da34-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="1da34-1079">3-50 (6)</span></span> |
| <span data-ttu-id="1da34-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="1da34-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="1da34-1081">界限 hello 頻繁的集合中的項目數目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="1da34-1082">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1082">Integer</span></span> |<span data-ttu-id="1da34-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="1da34-1083">2-3 (2)</span></span> |
| <span data-ttu-id="1da34-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="1da34-1084">FbtMinimalScore</span></span> |<span data-ttu-id="1da34-1085">基本分數頻繁集應該包含在 hello 順序 toobe 中傳回結果。</span><span class="sxs-lookup"><span data-stu-id="1da34-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="1da34-1086">hello 高 hello 更好。</span><span class="sxs-lookup"><span data-stu-id="1da34-1086">hello higher hello better.</span></span> |<span data-ttu-id="1da34-1087">Double</span><span class="sxs-lookup"><span data-stu-id="1da34-1087">Double</span></span> |<span data-ttu-id="1da34-1088">0 以上 (0)</span><span class="sxs-lookup"><span data-stu-id="1da34-1088">0 and above (0)</span></span> |
| <span data-ttu-id="1da34-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="1da34-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="1da34-1090">定義 hello 相似度函式 toobe hello 組建所使用。</span><span class="sxs-lookup"><span data-stu-id="1da34-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="1da34-1091">增益喜好 serendipity，共同出現喜好可預測性，且 Jaccard 之間 hello 兩個不錯的洩露。</span><span class="sxs-lookup"><span data-stu-id="1da34-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="1da34-1092">String</span><span class="sxs-lookup"><span data-stu-id="1da34-1092">String</span></span> |<span data-ttu-id="1da34-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="1da34-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="1da34-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-1094">11.2.</span></span> <span data-ttu-id="1da34-1095">觸發建議組建</span><span class="sxs-lookup"><span data-stu-id="1da34-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="1da34-1096">根據預設，此 API 會觸發建議模型組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="1da34-1097">tootrigger 陣序規範組建 （在順序 tooscore 功能），應使用 hello 建置應用程式開發介面 variant 組建的型別參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="1da34-1098">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1098">HTTP Method</span></span> | <span data-ttu-id="1da34-1099">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1100">POST</span><span class="sxs-lookup"><span data-stu-id="1da34-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1101">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="1da34-1102">標頭</span><span class="sxs-lookup"><span data-stu-id="1da34-1102">HEADER</span></span> |<span data-ttu-id="1da34-1103">`"Content-Type", "text/xml"` (如果傳送要求本文)</span><span class="sxs-lookup"><span data-stu-id="1da34-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="1da34-1104">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1104">Parameter Name</span></span> | <span data-ttu-id="1da34-1105">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1106">modelId</span></span> |<span data-ttu-id="1da34-1107">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="1da34-1108">userDescription</span></span> |<span data-ttu-id="1da34-1109">文字 hello 目錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="1da34-1110">請注意，如果您使用空格，必須將其編碼改成 %20。</span><span class="sxs-lookup"><span data-stu-id="1da34-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="1da34-1111">請參閱上面的範例。</span><span class="sxs-lookup"><span data-stu-id="1da34-1111">See example above.</span></span><br><span data-ttu-id="1da34-1112"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="1da34-1112">Max length: 50</span></span> |
| <span data-ttu-id="1da34-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1113">apiVersion</span></span> |<span data-ttu-id="1da34-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-1115">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-1115">Request Body</span></span> |<span data-ttu-id="1da34-1116">如果保留空白 hello 組建將會執行與 hello 預設組建參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="1da34-1117">如果您想 tooset hello 組建參數，請以 XML 傳送 hello 參數為 hello 如 hello 下列範例所示的本文。</span><span class="sxs-lookup"><span data-stu-id="1da34-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="1da34-1118">（請參閱 hello < 組建參數 > 一節說明 hello 參數）。`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="1da34-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="1da34-1119">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-1119">**Response**:</span></span>

<span data-ttu-id="1da34-1120">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1121">這是非同步的 API。</span><span class="sxs-lookup"><span data-stu-id="1da34-1121">This is an asynchronous API.</span></span> <span data-ttu-id="1da34-1122">您會得到一個組建識別碼做為回應。</span><span class="sxs-lookup"><span data-stu-id="1da34-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="1da34-1123">tooknow hello 建置結束時，您應該呼叫 hello 「 取得組建狀態的模型 」 應用程式開發介面，並找出這個組建 ID hello 回應中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="1da34-1124">請注意，組建可以從分鐘 toohours hello hello 資料大小而定。</span><span class="sxs-lookup"><span data-stu-id="1da34-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="1da34-1125">您無法使用建議，直到 hello 建置結束。</span><span class="sxs-lookup"><span data-stu-id="1da34-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="1da34-1126">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="1da34-1126">Valid build status:</span></span>

* <span data-ttu-id="1da34-1127">建立 - 組建要求已建立。</span><span class="sxs-lookup"><span data-stu-id="1da34-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="1da34-1128">已排入佇列 - 組建要求已傳送並排入佇列。</span><span class="sxs-lookup"><span data-stu-id="1da34-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="1da34-1129">建置中 - 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="1da34-1130">成功 - 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="1da34-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="1da34-1131">錯誤 - 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="1da34-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="1da34-1132">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="1da34-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="1da34-1133">取消-已傳送 hello 組建的取消要求。</span><span class="sxs-lookup"><span data-stu-id="1da34-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="1da34-1134">請注意可以在 hello 下列路徑下找到 ID 該 hello 組建：`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="1da34-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="1da34-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1135">OData XML</span></span>

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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="1da34-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-1136">11.3.</span></span> <span data-ttu-id="1da34-1137">觸發組建 (建議、排名或 FBT)</span><span class="sxs-lookup"><span data-stu-id="1da34-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="1da34-1138">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1138">HTTP Method</span></span> | <span data-ttu-id="1da34-1139">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1140">POST</span><span class="sxs-lookup"><span data-stu-id="1da34-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1141">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="1da34-1142">標頭</span><span class="sxs-lookup"><span data-stu-id="1da34-1142">HEADER</span></span> |<span data-ttu-id="1da34-1143">`"Content-Type", "text/xml"` (如果傳送要求本文)</span><span class="sxs-lookup"><span data-stu-id="1da34-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="1da34-1144">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1144">Parameter Name</span></span> | <span data-ttu-id="1da34-1145">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1146">modelId</span></span> |<span data-ttu-id="1da34-1147">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="1da34-1148">userDescription</span></span> |<span data-ttu-id="1da34-1149">文字 hello 目錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="1da34-1150">請注意，如果您使用空格，必須將其編碼改成 %20。</span><span class="sxs-lookup"><span data-stu-id="1da34-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="1da34-1151">請參閱上面的範例。</span><span class="sxs-lookup"><span data-stu-id="1da34-1151">See example above.</span></span><br><span data-ttu-id="1da34-1152"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="1da34-1152">Max length: 50</span></span> |
| <span data-ttu-id="1da34-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="1da34-1153">buildType</span></span> |<span data-ttu-id="1da34-1154">Hello 組建 tooinvoke 類型：</span><span class="sxs-lookup"><span data-stu-id="1da34-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="1da34-1155">- 'Recommendation' 為建議組建</span><span class="sxs-lookup"><span data-stu-id="1da34-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="1da34-1156">- 'Ranking' 為排名組建</span><span class="sxs-lookup"><span data-stu-id="1da34-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="1da34-1157"> - 'Fbt' 為 FBT 組建</span><span class="sxs-lookup"><span data-stu-id="1da34-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="1da34-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1158">apiVersion</span></span> |<span data-ttu-id="1da34-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-1160">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-1160">Request Body</span></span> |<span data-ttu-id="1da34-1161">如果保留空白 hello 組建將會執行與 hello 預設組建參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="1da34-1162">如果您想 tooset 組建參數，它們以傳送 XML 到像 hello 遵循範例中的 hello 主體。</span><span class="sxs-lookup"><span data-stu-id="1da34-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="1da34-1163">（請參閱 hello 「 組建參數 」 一節的說明，以及 hello 參數的完整清單）。`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="1da34-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="1da34-1164">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-1164">**Response**:</span></span>

<span data-ttu-id="1da34-1165">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1166">這是非同步的 API。</span><span class="sxs-lookup"><span data-stu-id="1da34-1166">This is an asynchronous API.</span></span> <span data-ttu-id="1da34-1167">您會得到一個組建識別碼做為回應。</span><span class="sxs-lookup"><span data-stu-id="1da34-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="1da34-1168">tooknow hello 建置結束時，您應該呼叫 hello 「 取得組建狀態的模型 」 應用程式開發介面，並找出這個組建 ID hello 回應中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="1da34-1169">請注意，組建可以從分鐘 toohours hello hello 資料大小而定。</span><span class="sxs-lookup"><span data-stu-id="1da34-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="1da34-1170">您無法使用建議，直到 hello 建置結束。</span><span class="sxs-lookup"><span data-stu-id="1da34-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="1da34-1171">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="1da34-1171">Valid build status:</span></span>

* <span data-ttu-id="1da34-1172">建立 - 模型已建立。</span><span class="sxs-lookup"><span data-stu-id="1da34-1172">Create - Model was created.</span></span>
* <span data-ttu-id="1da34-1173">已排入佇列 - 已觸發模型組建，並已排入佇列。</span><span class="sxs-lookup"><span data-stu-id="1da34-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="1da34-1174">建置中 - 模型正在建置中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="1da34-1175">成功 - 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="1da34-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="1da34-1176">錯誤 - 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="1da34-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="1da34-1177">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="1da34-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="1da34-1178">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="1da34-1179">請注意可以在 hello 下列路徑下找到 ID 該 hello 組建：`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="1da34-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="1da34-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1180">OData XML</span></span>

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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="1da34-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="1da34-1181">11.4.</span></span> <span data-ttu-id="1da34-1182">取得模型的組建狀態</span><span class="sxs-lookup"><span data-stu-id="1da34-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="1da34-1183">擷取指定之模型的組建及其狀態。</span><span class="sxs-lookup"><span data-stu-id="1da34-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="1da34-1184">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1184">HTTP Method</span></span> | <span data-ttu-id="1da34-1185">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1186">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1187">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1188">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1188">Parameter Name</span></span> | <span data-ttu-id="1da34-1189">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1190">modelId</span></span> |<span data-ttu-id="1da34-1191">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="1da34-1192">onlyLastBuild</span></span> |<span data-ttu-id="1da34-1193">表示所有 hello 的 tooreturn 建置 hello 模型的歷程記錄] 或 [僅 hello 狀態的 hello 最新的組建</span><span class="sxs-lookup"><span data-stu-id="1da34-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="1da34-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1194">apiVersion</span></span> |<span data-ttu-id="1da34-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1195">1.0</span></span> |

<span data-ttu-id="1da34-1196">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-1196">**Response**:</span></span>

<span data-ttu-id="1da34-1197">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1198">hello 回應會包含每一組建的一個項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="1da34-1199">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1200">`feed/entry/content/properties/UserName`-Hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="1da34-1201">`feed/entry/content/properties/ModelName`-Hello 模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="1da34-1202">`feed/entry/content/properties/ModelId` - 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="1da34-1203">`feed/entry/content/properties/IsDeployed`-Hello 組建是否部署 （也稱為</span><span class="sxs-lookup"><span data-stu-id="1da34-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="1da34-1204">作用中組建)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1204">active build).</span></span>
* <span data-ttu-id="1da34-1205">`feed/entry/content/properties/BuildId` - 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="1da34-1206">`feed/entry/content/properties/BuildType`Hello 組建的型別。</span><span class="sxs-lookup"><span data-stu-id="1da34-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="1da34-1207">`feed/entry/content/properties/Status` - 組建狀態。</span><span class="sxs-lookup"><span data-stu-id="1da34-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="1da34-1208">可以是 hello 下列其中一種： 錯誤、 建置、 排入佇列，正在取消、 取消、 成功。</span><span class="sxs-lookup"><span data-stu-id="1da34-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="1da34-1209">`feed/entry/content/properties/StatusMessage`-詳細狀態訊息 （適用於僅 toospecific 狀態）。</span><span class="sxs-lookup"><span data-stu-id="1da34-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="1da34-1210">`feed/entry/content/properties/Progress` - 組建進度 (%)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="1da34-1211">`feed/entry/content/properties/StartTime` - 組建開始時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="1da34-1212">`feed/entry/content/properties/EndTime` - 組建結束時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="1da34-1213">`feed/entry/content/properties/ExecutionTime` - 組建持續時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="1da34-1214">`feed/entry/content/properties/ProgressStep`組建正在進行中的 hello 目前階段的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="1da34-1215">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="1da34-1215">Valid build status:</span></span>

* <span data-ttu-id="1da34-1216">建立 - 組建要求項目已建立。</span><span class="sxs-lookup"><span data-stu-id="1da34-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="1da34-1217">已排入佇列 - 組建要求已觸發並排入佇列。</span><span class="sxs-lookup"><span data-stu-id="1da34-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="1da34-1218">建置中 - 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="1da34-1219">成功 - 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="1da34-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="1da34-1220">錯誤 - 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="1da34-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="1da34-1221">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="1da34-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="1da34-1222">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="1da34-1223">組建類型的有效值：</span><span class="sxs-lookup"><span data-stu-id="1da34-1223">Valid values for build type:</span></span>

* <span data-ttu-id="1da34-1224">排名 - 排名組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="1da34-1225">建議 - 建議組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="1da34-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1226">OData XML</span></span>

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


### <a name="115-get-builds-status"></a><span data-ttu-id="1da34-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="1da34-1227">11.5.</span></span> <span data-ttu-id="1da34-1228">取得組建狀態</span><span class="sxs-lookup"><span data-stu-id="1da34-1228">Get Builds Status</span></span>
<span data-ttu-id="1da34-1229">擷取使用者之所有模型的組建狀態。</span><span class="sxs-lookup"><span data-stu-id="1da34-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="1da34-1230">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1230">HTTP Method</span></span> | <span data-ttu-id="1da34-1231">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1232">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1233">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1234">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1234">Parameter Name</span></span> | <span data-ttu-id="1da34-1235">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="1da34-1236">onlyLastBuild</span></span> |<span data-ttu-id="1da34-1237">表示所有 hello 的 tooreturn 建置 hello 模型的歷程記錄] 或 [僅 hello 狀態的 hello 最新的組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="1da34-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1238">apiVersion</span></span> |<span data-ttu-id="1da34-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1239">1.0</span></span> |

<span data-ttu-id="1da34-1240">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-1240">**Response**:</span></span>

<span data-ttu-id="1da34-1241">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1242">hello 回應會包含每一組建的一個項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="1da34-1243">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1244">`feed/entry/content/properties/UserName`-Hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="1da34-1245">`feed/entry/content/properties/ModelName`-Hello 模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="1da34-1246">`feed/entry/content/properties/ModelId` - 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="1da34-1247">`feed/entry/content/properties/IsDeployed`-是否部署 hello 組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="1da34-1248">`feed/entry/content/properties/BuildId` - 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="1da34-1249">`feed/entry/content/properties/BuildType`Hello 組建的型別。</span><span class="sxs-lookup"><span data-stu-id="1da34-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="1da34-1250">`feed/entry/content/properties/Status` - 組建狀態。</span><span class="sxs-lookup"><span data-stu-id="1da34-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="1da34-1251">可以是 hello 下列其中一種： 錯誤、 建置、 已佇列、 已取消，正在取消、 成功。</span><span class="sxs-lookup"><span data-stu-id="1da34-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="1da34-1252">`feed/entry/content/properties/StatusMessage`-詳細狀態訊息 （適用於僅 toospecific 狀態）。</span><span class="sxs-lookup"><span data-stu-id="1da34-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="1da34-1253">`feed/entry/content/properties/Progress` - 組建進度 (%)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="1da34-1254">`feed/entry/content/properties/StartTime` - 組建開始時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="1da34-1255">`feed/entry/content/properties/EndTime` - 組建結束時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="1da34-1256">`feed/entry/content/properties/ExecutionTime` - 組建持續時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="1da34-1257">`feed/entry/content/properties/ProgressStep`組建正在進行中的 hello 目前階段的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1da34-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="1da34-1258">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="1da34-1258">Valid build status:</span></span>

* <span data-ttu-id="1da34-1259">建立 - 組建要求項目已建立。</span><span class="sxs-lookup"><span data-stu-id="1da34-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="1da34-1260">已排入佇列 - 組建要求已觸發並排入佇列。</span><span class="sxs-lookup"><span data-stu-id="1da34-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="1da34-1261">建置中 - 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="1da34-1262">成功 - 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="1da34-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="1da34-1263">錯誤 - 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="1da34-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="1da34-1264">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="1da34-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="1da34-1265">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="1da34-1266">組建類型的有效值：</span><span class="sxs-lookup"><span data-stu-id="1da34-1266">Valid values for build type:</span></span>

* <span data-ttu-id="1da34-1267">排名 - 排名組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="1da34-1268">建議 - 建議組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="1da34-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1269">OData XML</span></span>

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


### <a name="116-delete-build"></a><span data-ttu-id="1da34-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="1da34-1270">11.6.</span></span> <span data-ttu-id="1da34-1271">刪除組建</span><span class="sxs-lookup"><span data-stu-id="1da34-1271">Delete Build</span></span>
<span data-ttu-id="1da34-1272">刪除組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1272">Deletes a build.</span></span>

<span data-ttu-id="1da34-1273">注意：</span><span class="sxs-lookup"><span data-stu-id="1da34-1273">NOTE:</span></span> <br><span data-ttu-id="1da34-1274">您無法刪除使用中組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1274">You cannot delete an active build.</span></span> <span data-ttu-id="1da34-1275">hello 模型應該更新 tooa 其他作用中的組建，然後再刪除它。</span><span class="sxs-lookup"><span data-stu-id="1da34-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="1da34-1276">您無法刪除進行中組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="1da34-1277">您應該先取消 hello 組建，藉由呼叫<strong>取消建置</strong>。</span><span class="sxs-lookup"><span data-stu-id="1da34-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="1da34-1278">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1278">HTTP Method</span></span> | <span data-ttu-id="1da34-1279">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1280">刪除</span><span class="sxs-lookup"><span data-stu-id="1da34-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1281">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1282">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1282">Parameter Name</span></span> | <span data-ttu-id="1da34-1283">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-1284">buildId</span></span> |<span data-ttu-id="1da34-1285">Hello 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="1da34-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1286">apiVersion</span></span> |<span data-ttu-id="1da34-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1287">1.0</span></span> |

<span data-ttu-id="1da34-1288">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1288">**Response:**</span></span>

<span data-ttu-id="1da34-1289">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="1da34-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="1da34-1290">11.7.</span></span> <span data-ttu-id="1da34-1291">取消組建</span><span class="sxs-lookup"><span data-stu-id="1da34-1291">Cancel Build</span></span>
<span data-ttu-id="1da34-1292">取消狀態為建置中的組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="1da34-1293">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1293">HTTP Method</span></span> | <span data-ttu-id="1da34-1294">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="1da34-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1296">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1297">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1297">Parameter Name</span></span> | <span data-ttu-id="1da34-1298">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-1299">buildId</span></span> |<span data-ttu-id="1da34-1300">Hello 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="1da34-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1301">apiVersion</span></span> |<span data-ttu-id="1da34-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1302">1.0</span></span> |

<span data-ttu-id="1da34-1303">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1303">**Response:**</span></span>

<span data-ttu-id="1da34-1304">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="1da34-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="1da34-1305">11.8.</span></span> <span data-ttu-id="1da34-1306">取得組建參數</span><span class="sxs-lookup"><span data-stu-id="1da34-1306">Get Build Parameters</span></span>
<span data-ttu-id="1da34-1307">擷取組建參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="1da34-1308">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1308">HTTP Method</span></span> | <span data-ttu-id="1da34-1309">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1310">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1311">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1312">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1312">Parameter Name</span></span> | <span data-ttu-id="1da34-1313">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-1314">buildId</span></span> |<span data-ttu-id="1da34-1315">Hello 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="1da34-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1316">apiVersion</span></span> |<span data-ttu-id="1da34-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1317">1.0</span></span> |

<span data-ttu-id="1da34-1318">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1318">**Response:**</span></span>

<span data-ttu-id="1da34-1319">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1320">此 API 會傳回索引鍵/值項目的集合。</span><span class="sxs-lookup"><span data-stu-id="1da34-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="1da34-1321">每個元素都代表參數和它的值：</span><span class="sxs-lookup"><span data-stu-id="1da34-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="1da34-1322">`feed/entry/content/properties/Key` - 組建參數名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="1da34-1323">`feed/entry/content/properties/Value` - 組建參數值。</span><span class="sxs-lookup"><span data-stu-id="1da34-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="1da34-1324">hello 下表描述每個索引鍵所代表的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="1da34-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="1da34-1325">Key</span><span class="sxs-lookup"><span data-stu-id="1da34-1325">Key</span></span> | <span data-ttu-id="1da34-1326">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-1326">Description</span></span> | <span data-ttu-id="1da34-1327">類型</span><span class="sxs-lookup"><span data-stu-id="1da34-1327">Type</span></span> | <span data-ttu-id="1da34-1328">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1da34-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="1da34-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="1da34-1330">hello 數目 hello 模型執行的反覆項目都會反映在 hello 整體計算時間和 hello 模型精確度。</span><span class="sxs-lookup"><span data-stu-id="1da34-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="1da34-1331">hello hello 編號，hello 更好的精確度，您會收到，但是 hello 計算需要較久的時間。</span><span class="sxs-lookup"><span data-stu-id="1da34-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="1da34-1332">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1332">Integer</span></span> |<span data-ttu-id="1da34-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="1da34-1333">10-50</span></span> |
| <span data-ttu-id="1da34-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="1da34-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="1da34-1335">維度的 hello 數目相關 toohello '功能' hello 模型數目將會嘗試 toofind 資料中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="1da34-1336">增加 hello 維度的數目，可讓更好，微調 hello 結果分成較小的群集。</span><span class="sxs-lookup"><span data-stu-id="1da34-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="1da34-1337">但是，太多維度會防止 hello 模型尋找項目之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="1da34-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="1da34-1338">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1338">Integer</span></span> |<span data-ttu-id="1da34-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="1da34-1339">10-40</span></span> |
| <span data-ttu-id="1da34-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="1da34-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="1da34-1341">定義 hello hello 冷凝器的項目下限。</span><span class="sxs-lookup"><span data-stu-id="1da34-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="1da34-1342">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1342">See usage condenser above.</span></span> |<span data-ttu-id="1da34-1343">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1343">Integer</span></span> |<span data-ttu-id="1da34-1344">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="1da34-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="1da34-1346">定義 hello hello 冷凝器的項目上限。</span><span class="sxs-lookup"><span data-stu-id="1da34-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="1da34-1347">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1347">See usage condenser above.</span></span> |<span data-ttu-id="1da34-1348">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1348">Integer</span></span> |<span data-ttu-id="1da34-1349">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="1da34-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="1da34-1351">定義 hello 使用者下限 hello 冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="1da34-1352">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1352">See usage condenser above.</span></span> |<span data-ttu-id="1da34-1353">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1353">Integer</span></span> |<span data-ttu-id="1da34-1354">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="1da34-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="1da34-1356">定義 hello 使用者上限 hello 冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="1da34-1357">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="1da34-1357">See usage condenser above.</span></span> |<span data-ttu-id="1da34-1358">Integer</span><span class="sxs-lookup"><span data-stu-id="1da34-1358">Integer</span></span> |<span data-ttu-id="1da34-1359">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="1da34-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="1da34-1360">說明</span><span class="sxs-lookup"><span data-stu-id="1da34-1360">Description</span></span> |<span data-ttu-id="1da34-1361">建置說明。</span><span class="sxs-lookup"><span data-stu-id="1da34-1361">Build description.</span></span> |<span data-ttu-id="1da34-1362">String</span><span class="sxs-lookup"><span data-stu-id="1da34-1362">String</span></span> |<span data-ttu-id="1da34-1363">任何文字，最多 512 個字元</span><span class="sxs-lookup"><span data-stu-id="1da34-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="1da34-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="1da34-1364">EnableModelingInsights</span></span> |<span data-ttu-id="1da34-1365">可讓您 toocompute 度量 hello 推薦模型上。</span><span class="sxs-lookup"><span data-stu-id="1da34-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="1da34-1366">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1366">Boolean</span></span> |<span data-ttu-id="1da34-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="1da34-1367">True/False</span></span> |
| <span data-ttu-id="1da34-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="1da34-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="1da34-1369">指出功能是否可以使用順序 tooenhance hello 建議模型中。</span><span class="sxs-lookup"><span data-stu-id="1da34-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="1da34-1370">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1370">Boolean</span></span> |<span data-ttu-id="1da34-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="1da34-1371">True/False</span></span> |
| <span data-ttu-id="1da34-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="1da34-1372">ModelingFeatureList</span></span> |<span data-ttu-id="1da34-1373">功能名稱 toobe 順序 tooenhance hello 建議事項中的 hello 建議組建中使用的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="1da34-1374">String</span><span class="sxs-lookup"><span data-stu-id="1da34-1374">String</span></span> |<span data-ttu-id="1da34-1375">Too512 字元組成的功能名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="1da34-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="1da34-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="1da34-1377">指出是否 hello 建議也應該推送的陌生項目透過功能相似。</span><span class="sxs-lookup"><span data-stu-id="1da34-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="1da34-1378">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1378">Boolean</span></span> |<span data-ttu-id="1da34-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="1da34-1379">True/False</span></span> |
| <span data-ttu-id="1da34-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="1da34-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="1da34-1381">指出功能是否可用於推論。</span><span class="sxs-lookup"><span data-stu-id="1da34-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="1da34-1382">Boolean</span><span class="sxs-lookup"><span data-stu-id="1da34-1382">Boolean</span></span> |<span data-ttu-id="1da34-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="1da34-1383">True/False</span></span> |
| <span data-ttu-id="1da34-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="1da34-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="1da34-1385">以逗號分隔清單的功能名稱 toobe 用於推理句子 （例如建議說明）。</span><span class="sxs-lookup"><span data-stu-id="1da34-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="1da34-1386">String</span><span class="sxs-lookup"><span data-stu-id="1da34-1386">String</span></span> |<span data-ttu-id="1da34-1387">Too512 字元組成的功能名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="1da34-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1388">OData XML</span></span>

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

## <a name="12-recommendation"></a><span data-ttu-id="1da34-1389">12.建議</span><span class="sxs-lookup"><span data-stu-id="1da34-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="1da34-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-1390">12.1.</span></span> <span data-ttu-id="1da34-1391">取得項目建議 (適用於作用中組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="1da34-1392">取得建議的 hello 作用中的組建類型的 「 建議事項 」 或者 「 Fbt"根據種子 （輸入） 項目清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="1da34-1393">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1393">HTTP Method</span></span> | <span data-ttu-id="1da34-1394">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1395">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1396">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1397">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1397">Parameter Name</span></span> | <span data-ttu-id="1da34-1398">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1399">modelId</span></span> |<span data-ttu-id="1da34-1400">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="1da34-1401">itemIds</span></span> |<span data-ttu-id="1da34-1402">以逗號分隔的 hello 項目 toorecommend 的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="1da34-1403">如果 hello active 組建的輸入 FBT，則您可以傳送只有一個項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="1da34-1404">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="1da34-1404">Max length: 1024</span></span> |
| <span data-ttu-id="1da34-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1da34-1405">numberOfResults</span></span> |<span data-ttu-id="1da34-1406">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="1da34-1406">Number of required results</span></span> <br> <span data-ttu-id="1da34-1407"> 最大值：150</span><span class="sxs-lookup"><span data-stu-id="1da34-1407">Max: 150</span></span> |
| <span data-ttu-id="1da34-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1da34-1408">includeMetatadata</span></span> |<span data-ttu-id="1da34-1409">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="1da34-1409">Future use, always false</span></span> |
| <span data-ttu-id="1da34-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1410">apiVersion</span></span> |<span data-ttu-id="1da34-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1411">1.0</span></span> |

<span data-ttu-id="1da34-1412">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1412">**Response:**</span></span>

<span data-ttu-id="1da34-1413">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1414">hello 回應包含一個項目，每個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="1da34-1415">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1416">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1417">`Feed\entry\content\properties\Name`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1418">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="1da34-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1da34-1419">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="1da34-1420">以下的 hello 範例回應會包含 10 個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="1da34-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1421">OData XML</span></span>

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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="1da34-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-1422">12.2.</span></span> <span data-ttu-id="1da34-1423">取得項目建議 (屬於特定組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="1da34-1424">取得 "Recommendation" 或 "Fbt" 等類型之特定組建的建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="1da34-1425">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1425">HTTP Method</span></span> | <span data-ttu-id="1da34-1426">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1427">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1428">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1429">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1429">Parameter Name</span></span> | <span data-ttu-id="1da34-1430">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1431">modelId</span></span> |<span data-ttu-id="1da34-1432">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="1da34-1433">itemIds</span></span> |<span data-ttu-id="1da34-1434">以逗號分隔的 hello 項目 toorecommend 的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="1da34-1435">如果 hello active 組建的輸入 FBT，則您可以傳送只有一個項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="1da34-1436">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="1da34-1436">Max length: 1024</span></span> |
| <span data-ttu-id="1da34-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1da34-1437">numberOfResults</span></span> |<span data-ttu-id="1da34-1438">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="1da34-1438">Number of required results</span></span> <br> <span data-ttu-id="1da34-1439"> 最大值：150</span><span class="sxs-lookup"><span data-stu-id="1da34-1439">Max: 150</span></span> |
| <span data-ttu-id="1da34-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1da34-1440">includeMetatadata</span></span> |<span data-ttu-id="1da34-1441">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="1da34-1441">Future use, always false</span></span> |
| <span data-ttu-id="1da34-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-1442">buildId</span></span> |<span data-ttu-id="1da34-1443">hello 建置此建議要求識別碼 toouse</span><span class="sxs-lookup"><span data-stu-id="1da34-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="1da34-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1444">apiVersion</span></span> |<span data-ttu-id="1da34-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1445">1.0</span></span> |

<span data-ttu-id="1da34-1446">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1446">**Response:**</span></span>

<span data-ttu-id="1da34-1447">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1448">hello 回應包含一個項目，每個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="1da34-1449">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1450">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1451">`Feed\entry\content\properties\Name`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1452">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="1da34-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1da34-1453">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="1da34-1454">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="1da34-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="1da34-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-1455">12.3.</span></span> <span data-ttu-id="1da34-1456">取得 FBT 建議 (適用於作用中組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="1da34-1457">收到 hello"Fbt 」 為基礎的種子 （輸入） 項目類型的使用中的組建的建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="1da34-1458">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1458">HTTP Method</span></span> | <span data-ttu-id="1da34-1459">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1460">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1461">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1462">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1462">Parameter Name</span></span> | <span data-ttu-id="1da34-1463">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1464">modelId</span></span> |<span data-ttu-id="1da34-1465">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="1da34-1466">itemId</span></span> |<span data-ttu-id="1da34-1467">項目 toorecommend。</span><span class="sxs-lookup"><span data-stu-id="1da34-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="1da34-1468">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="1da34-1468">Max length: 1024</span></span> |
| <span data-ttu-id="1da34-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1da34-1469">numberOfResults</span></span> |<span data-ttu-id="1da34-1470">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="1da34-1470">Number of required results</span></span> <br><span data-ttu-id="1da34-1471"> 最大值：150</span><span class="sxs-lookup"><span data-stu-id="1da34-1471">Max: 150</span></span> |
| <span data-ttu-id="1da34-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="1da34-1472">minimalScore</span></span> |<span data-ttu-id="1da34-1473">基本分數頻繁集應該包含在 hello 順序 toobe 中傳回結果</span><span class="sxs-lookup"><span data-stu-id="1da34-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="1da34-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1da34-1474">includeMetatadata</span></span> |<span data-ttu-id="1da34-1475">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="1da34-1475">Future use, always false</span></span> |
| <span data-ttu-id="1da34-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1476">apiVersion</span></span> |<span data-ttu-id="1da34-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1477">1.0</span></span> |

<span data-ttu-id="1da34-1478">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1478">**Response:**</span></span>

<span data-ttu-id="1da34-1479">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1480">hello 回應會包含每個建議的項目集 （通常與 hello 種子/輸入項目一起購買的項目組） 的一個項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="1da34-1481">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1482">`Feed\entry\content\properties\Id1` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1483">`Feed\entry\content\properties\Name1`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1484">`Feed\entry\content\properties\Id2` - 第二個建議項目的識別碼 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="1da34-1485">`Feed\entry\content\properties\Name2`-Hello 第 2 個項目 （選擇性） 名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="1da34-1486">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="1da34-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1da34-1487">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="1da34-1488">hello 以下的範例回應會包含 3 的建議項目組。</span><span class="sxs-lookup"><span data-stu-id="1da34-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="1da34-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1489">OData XML</span></span>

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

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="1da34-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="1da34-1490">12.4.</span></span> <span data-ttu-id="1da34-1491">取得 FBT 建議 (屬於特定組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="1da34-1492">取得 "Fbt" 類型之特定組建的建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="1da34-1493">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1493">HTTP Method</span></span> | <span data-ttu-id="1da34-1494">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1495">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1496">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1497">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1497">Parameter Name</span></span> | <span data-ttu-id="1da34-1498">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1499">modelId</span></span> |<span data-ttu-id="1da34-1500">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="1da34-1501">itemId</span></span> |<span data-ttu-id="1da34-1502">項目 toorecommend。</span><span class="sxs-lookup"><span data-stu-id="1da34-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="1da34-1503">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="1da34-1503">Max length: 1024</span></span> |
| <span data-ttu-id="1da34-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1da34-1504">numberOfResults</span></span> |<span data-ttu-id="1da34-1505">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="1da34-1505">Number of required results</span></span> <br><span data-ttu-id="1da34-1506"> 最大值：150</span><span class="sxs-lookup"><span data-stu-id="1da34-1506">Max: 150</span></span> |
| <span data-ttu-id="1da34-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="1da34-1507">minimalScore</span></span> |<span data-ttu-id="1da34-1508">基本分數頻繁集應該包含在 hello 順序 toobe 中傳回結果</span><span class="sxs-lookup"><span data-stu-id="1da34-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="1da34-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1da34-1509">includeMetatadata</span></span> |<span data-ttu-id="1da34-1510">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="1da34-1510">Future use, always false</span></span> |
| <span data-ttu-id="1da34-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-1511">buildId</span></span> |<span data-ttu-id="1da34-1512">hello 建置此建議要求識別碼 toouse</span><span class="sxs-lookup"><span data-stu-id="1da34-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="1da34-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1513">apiVersion</span></span> |<span data-ttu-id="1da34-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1514">1.0</span></span> |

<span data-ttu-id="1da34-1515">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1515">**Response:**</span></span>

<span data-ttu-id="1da34-1516">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1517">hello 回應會包含每個建議的項目集 （通常與 hello 種子/輸入項目一起購買的項目組） 的一個項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="1da34-1518">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1519">`Feed\entry\content\properties\Id1` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1520">`Feed\entry\content\properties\Name1`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1521">`Feed\entry\content\properties\Id2` - 第二個建議項目的識別碼 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="1da34-1522">`Feed\entry\content\properties\Name2`-Hello 第 2 個項目 （選擇性） 名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="1da34-1523">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="1da34-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1da34-1524">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="1da34-1525">請參閱 12.3 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="1da34-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="1da34-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="1da34-1526">12.5.</span></span> <span data-ttu-id="1da34-1527">取得使用者建議 (適用於作用中組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="1da34-1528">取得標示為作用中組建之 "Recommendation" 類型之組建的使用者建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="1da34-1529">hello API 會傳回一份根據 hello 使用者 toohello 使用量歷程記錄預測的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="1da34-1530">注意：</span><span class="sxs-lookup"><span data-stu-id="1da34-1530">Notes:</span></span> 

1. <span data-ttu-id="1da34-1531">FBT 組建沒有使用者建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="1da34-1532">如果使用中的 hello 建置是的 FBT 這個方法會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="1da34-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="1da34-1533">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1533">HTTP Method</span></span> | <span data-ttu-id="1da34-1534">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1535">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1536">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1537">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1537">Parameter Name</span></span> | <span data-ttu-id="1da34-1538">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1539">modelId</span></span> |<span data-ttu-id="1da34-1540">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1541">userId</span><span class="sxs-lookup"><span data-stu-id="1da34-1541">userId</span></span> |<span data-ttu-id="1da34-1542">Hello 使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="1da34-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1da34-1543">numberOfResults</span></span> |<span data-ttu-id="1da34-1544">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="1da34-1544">Number of required results</span></span> |
| <span data-ttu-id="1da34-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1da34-1545">includeMetatadata</span></span> |<span data-ttu-id="1da34-1546">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="1da34-1546">Future use, always false</span></span> |
| <span data-ttu-id="1da34-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1547">apiVersion</span></span> |<span data-ttu-id="1da34-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1548">1.0</span></span> |

<span data-ttu-id="1da34-1549">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1549">**Response:**</span></span>

<span data-ttu-id="1da34-1550">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1551">hello 回應包含一個項目，每個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="1da34-1552">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1553">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1554">`Feed\entry\content\properties\Name`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1555">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="1da34-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1da34-1556">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="1da34-1557">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="1da34-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="1da34-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="1da34-1558">12.6.</span></span> <span data-ttu-id="1da34-1559">使用項目清單取得使用者建議 (適用於作用中組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="1da34-1560">使用額外的項目清單，取得標示為作用中組建之 "Recommendation" 類型之組建的使用者建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="1da34-1561">hello API 會傳回一份根據 hello 使用者和 hello 額外的提供的項目的 toohello 使用量歷程記錄預測的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="1da34-1562">注意：</span><span class="sxs-lookup"><span data-stu-id="1da34-1562">Notes:</span></span> 

1. <span data-ttu-id="1da34-1563">FBT 組建沒有使用者建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="1da34-1564">如果使用中的 hello 建置是的 FBT 這個方法會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="1da34-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="1da34-1565">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1565">HTTP Method</span></span> | <span data-ttu-id="1da34-1566">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1567">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1568">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1569">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1569">Parameter Name</span></span> | <span data-ttu-id="1da34-1570">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1571">modelId</span></span> |<span data-ttu-id="1da34-1572">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1573">userId</span><span class="sxs-lookup"><span data-stu-id="1da34-1573">userId</span></span> |<span data-ttu-id="1da34-1574">Hello 使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="1da34-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="1da34-1575">itemsIds</span></span> |<span data-ttu-id="1da34-1576">以逗號分隔的 hello 項目 toorecommend 的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="1da34-1577">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="1da34-1577">Max length: 1024</span></span> |
| <span data-ttu-id="1da34-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1da34-1578">numberOfResults</span></span> |<span data-ttu-id="1da34-1579">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="1da34-1579">Number of required results</span></span> |
| <span data-ttu-id="1da34-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1da34-1580">includeMetatadata</span></span> |<span data-ttu-id="1da34-1581">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="1da34-1581">Future use, always false</span></span> |
| <span data-ttu-id="1da34-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1582">apiVersion</span></span> |<span data-ttu-id="1da34-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1583">1.0</span></span> |

<span data-ttu-id="1da34-1584">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1584">**Response:**</span></span>

<span data-ttu-id="1da34-1585">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1586">hello 回應包含一個項目，每個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="1da34-1587">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1588">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1589">`Feed\entry\content\properties\Name`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1590">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="1da34-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1da34-1591">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="1da34-1592">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="1da34-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="1da34-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="1da34-1593">12.7.</span></span> <span data-ttu-id="1da34-1594">取得使用者建議 (屬於特定組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="1da34-1595">取得 "Recommendation" 類型之特定組建的使用者建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="1da34-1596">hello API 會傳回一份根據 toohello 使用量記錄 hello 使用者 （在 hello 特定組建中使用） 的預測的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="1da34-1597">注意：FBT 組建沒有使用者建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="1da34-1598">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1598">HTTP Method</span></span> | <span data-ttu-id="1da34-1599">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1600">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1601">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1602">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1602">Parameter Name</span></span> | <span data-ttu-id="1da34-1603">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1604">modelId</span></span> |<span data-ttu-id="1da34-1605">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1606">userId</span><span class="sxs-lookup"><span data-stu-id="1da34-1606">userId</span></span> |<span data-ttu-id="1da34-1607">Hello 使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="1da34-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1da34-1608">numberOfResults</span></span> |<span data-ttu-id="1da34-1609">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="1da34-1609">Number of required results</span></span> |
| <span data-ttu-id="1da34-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1da34-1610">includeMetatadata</span></span> |<span data-ttu-id="1da34-1611">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="1da34-1611">Future use, always false</span></span> |
| <span data-ttu-id="1da34-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-1612">buildId</span></span> |<span data-ttu-id="1da34-1613">hello 建置此建議要求識別碼 toouse</span><span class="sxs-lookup"><span data-stu-id="1da34-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="1da34-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1614">apiVersion</span></span> |<span data-ttu-id="1da34-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1615">1.0</span></span> |

<span data-ttu-id="1da34-1616">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1616">**Response:**</span></span>

<span data-ttu-id="1da34-1617">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1618">hello 回應包含一個項目，每個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="1da34-1619">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1620">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1621">`Feed\entry\content\properties\Name`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1622">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="1da34-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1da34-1623">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="1da34-1624">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="1da34-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="1da34-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="1da34-1625">12.8.</span></span> <span data-ttu-id="1da34-1626">使用項目清單取得使用者建議 (屬於特定組建)</span><span class="sxs-lookup"><span data-stu-id="1da34-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="1da34-1627">取得使用者的建議特定的組建的型別 [建議] 和其他項目 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="1da34-1628">hello API 會傳回預測的項目，根據 hello 使用者 toohello 使用量歷程記錄和 hello 其他項目清單的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="1da34-1629">注意：FBT 組建沒有使用者建議。</span><span class="sxs-lookup"><span data-stu-id="1da34-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="1da34-1630">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1630">HTTP Method</span></span> | <span data-ttu-id="1da34-1631">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1632">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1633">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1634">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1634">Parameter Name</span></span> | <span data-ttu-id="1da34-1635">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1636">modelId</span></span> |<span data-ttu-id="1da34-1637">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1638">userId</span><span class="sxs-lookup"><span data-stu-id="1da34-1638">userId</span></span> |<span data-ttu-id="1da34-1639">Hello 使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="1da34-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="1da34-1640">itemIds</span></span> |<span data-ttu-id="1da34-1641">以逗號分隔的 hello 項目 toorecommend 的清單。</span><span class="sxs-lookup"><span data-stu-id="1da34-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="1da34-1642">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="1da34-1642">Max length: 1024</span></span> |
| <span data-ttu-id="1da34-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1da34-1643">numberOfResults</span></span> |<span data-ttu-id="1da34-1644">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="1da34-1644">Number of required results</span></span> |
| <span data-ttu-id="1da34-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1da34-1645">includeMetatadata</span></span> |<span data-ttu-id="1da34-1646">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="1da34-1646">Future use, always false</span></span> |
| <span data-ttu-id="1da34-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-1647">buildId</span></span> |<span data-ttu-id="1da34-1648">hello 建置此建議要求識別碼 toouse</span><span class="sxs-lookup"><span data-stu-id="1da34-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="1da34-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1649">apiVersion</span></span> |<span data-ttu-id="1da34-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1650">1.0</span></span> |

<span data-ttu-id="1da34-1651">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1651">**Response:**</span></span>

<span data-ttu-id="1da34-1652">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1653">hello 回應包含一個項目，每個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="1da34-1654">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1655">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1656">`Feed\entry\content\properties\Name`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1657">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="1da34-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1da34-1658">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="1da34-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="1da34-1659">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="1da34-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="1da34-1660">13.使用者使用歷程記錄</span><span class="sxs-lookup"><span data-stu-id="1da34-1660">13. User Usage History</span></span>
<span data-ttu-id="1da34-1661">一旦推薦模型所建立 hello 系統將可允許 tooretrieve hello 的使用者歷程記錄 （項目相關聯的 tooa 特定使用者） 用於 hello 組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="1da34-1662">這個 API 允許 tooretrieve hello 的使用者歷程記錄</span><span class="sxs-lookup"><span data-stu-id="1da34-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="1da34-1663">注意： hello 的使用者歷程記錄是目前僅適用於建議組建。</span><span class="sxs-lookup"><span data-stu-id="1da34-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="1da34-1664">13.1 擷取使用者歷程記錄</span><span class="sxs-lookup"><span data-stu-id="1da34-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="1da34-1665">擷取 hello 清單用於 hello 作用中的項目建置，或在指定的 hello 建置指定的使用者 id 的 hello。</span><span class="sxs-lookup"><span data-stu-id="1da34-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="1da34-1666">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1666">HTTP Method</span></span> | <span data-ttu-id="1da34-1667">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1668">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1668">GET</span></span> |<span data-ttu-id="1da34-1669">取得 hello active 組建 hello 使用者歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="1da34-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="1da34-1670">取得指定組建的 hello hello 使用者歷程記錄`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="1da34-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="1da34-1671">範例：`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="1da34-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="1da34-1672">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1672">Parameter Name</span></span> | <span data-ttu-id="1da34-1673">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1674">modelId</span></span> |<span data-ttu-id="1da34-1675">hello hello 模型的唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="1da34-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="1da34-1676">userId</span><span class="sxs-lookup"><span data-stu-id="1da34-1676">userId</span></span> |<span data-ttu-id="1da34-1677">hello hello 使用者的唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="1da34-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="1da34-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="1da34-1678">buildId</span></span> |<span data-ttu-id="1da34-1679">選擇性參數，允許從組建 hello 的使用者歷程記錄應擷取 tooindicate</span><span class="sxs-lookup"><span data-stu-id="1da34-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="1da34-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1680">apiVersion</span></span> |<span data-ttu-id="1da34-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1681">1.0</span></span> |

<span data-ttu-id="1da34-1682">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1682">**Response:**</span></span>

<span data-ttu-id="1da34-1683">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1684">hello 回應包含一個項目，每個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="1da34-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="1da34-1685">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1da34-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="1da34-1686">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="1da34-1687">`Feed\entry\content\properties\Name`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1da34-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="1da34-1688">`Feed\entry\content\properties\Rating` - N/A。</span><span class="sxs-lookup"><span data-stu-id="1da34-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="1da34-1689">`Feed\entry\content\properties\Reasoning` - N/A。</span><span class="sxs-lookup"><span data-stu-id="1da34-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="1da34-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1690">OData XML</span></span>

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

## <a name="14-notifications"></a><span data-ttu-id="1da34-1691">14.通知</span><span class="sxs-lookup"><span data-stu-id="1da34-1691">14. Notifications</span></span>
<span data-ttu-id="1da34-1692">Azure 機器學習建議 hello 系統中的持續性錯誤發生時，會建立通知。</span><span class="sxs-lookup"><span data-stu-id="1da34-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="1da34-1693">有 3 種類型的通知：</span><span class="sxs-lookup"><span data-stu-id="1da34-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="1da34-1694">組建失敗 – 每個組建失敗都會觸發此通知。</span><span class="sxs-lookup"><span data-stu-id="1da34-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="1da34-1695">我們有超過 100 個錯誤中 hello hello 處理的每個模型的使用量事件中的前 5 分鐘觸發處理失敗-此通知的資料擷取。</span><span class="sxs-lookup"><span data-stu-id="1da34-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="1da34-1696">我們有超過 100 個錯誤中 hello hello 處理建議要求每個模型中的前 5 分鐘觸發建議耗用量失敗-此通知。</span><span class="sxs-lookup"><span data-stu-id="1da34-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="1da34-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="1da34-1697">14.1.</span></span> <span data-ttu-id="1da34-1698">取得通知</span><span class="sxs-lookup"><span data-stu-id="1da34-1698">Get Notifications</span></span>
<span data-ttu-id="1da34-1699">擷取所有 hello 通知所有模型或單一模型。</span><span class="sxs-lookup"><span data-stu-id="1da34-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="1da34-1700">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1700">HTTP Method</span></span> | <span data-ttu-id="1da34-1701">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1702">GET</span><span class="sxs-lookup"><span data-stu-id="1da34-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1703">取得所有模型的所有通知：</span><span class="sxs-lookup"><span data-stu-id="1da34-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1704">取得特定模型之通知的範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="1da34-1705">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1705">Parameter Name</span></span> | <span data-ttu-id="1da34-1706">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1707">modelId</span></span> |<span data-ttu-id="1da34-1708">選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="1da34-1708">Optional parameter.</span></span> <span data-ttu-id="1da34-1709">如果省略此參數，您將會取得所有模型的所有通知。</span><span class="sxs-lookup"><span data-stu-id="1da34-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="1da34-1710">有效值： hello 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1da34-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="1da34-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1711">apiVersion</span></span> |<span data-ttu-id="1da34-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-1713">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-1713">Request Body</span></span> |<span data-ttu-id="1da34-1714">無</span><span class="sxs-lookup"><span data-stu-id="1da34-1714">NONE</span></span> |

<span data-ttu-id="1da34-1715">**回應：**</span><span class="sxs-lookup"><span data-stu-id="1da34-1715">**Response:**</span></span>

<span data-ttu-id="1da34-1716">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="1da34-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="1da34-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
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

### <a name="142-delete-model-notifications"></a><span data-ttu-id="1da34-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="1da34-1718">14.2.</span></span> <span data-ttu-id="1da34-1719">刪除模型通知</span><span class="sxs-lookup"><span data-stu-id="1da34-1719">Delete Model Notifications</span></span>
<span data-ttu-id="1da34-1720">刪除模型的所有已讀通知。</span><span class="sxs-lookup"><span data-stu-id="1da34-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="1da34-1721">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1721">HTTP Method</span></span> | <span data-ttu-id="1da34-1722">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1723">刪除</span><span class="sxs-lookup"><span data-stu-id="1da34-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1da34-1724">範例：</span><span class="sxs-lookup"><span data-stu-id="1da34-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1725">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1725">Parameter Name</span></span> | <span data-ttu-id="1da34-1726">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="1da34-1727">modelId</span></span> |<span data-ttu-id="1da34-1728">Hello 模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="1da34-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="1da34-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1729">apiVersion</span></span> |<span data-ttu-id="1da34-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-1731">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-1731">Request Body</span></span> |<span data-ttu-id="1da34-1732">無</span><span class="sxs-lookup"><span data-stu-id="1da34-1732">NONE</span></span> |

<span data-ttu-id="1da34-1733">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-1733">**Response**:</span></span>

<span data-ttu-id="1da34-1734">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="1da34-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="1da34-1735">14.3.</span></span> <span data-ttu-id="1da34-1736">刪除使用者通知</span><span class="sxs-lookup"><span data-stu-id="1da34-1736">Delete User Notifications</span></span>
<span data-ttu-id="1da34-1737">刪除所有模型的所有通知。</span><span class="sxs-lookup"><span data-stu-id="1da34-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="1da34-1738">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1da34-1738">HTTP Method</span></span> | <span data-ttu-id="1da34-1739">URI</span><span class="sxs-lookup"><span data-stu-id="1da34-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1740">刪除</span><span class="sxs-lookup"><span data-stu-id="1da34-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="1da34-1741">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1da34-1741">Parameter Name</span></span> | <span data-ttu-id="1da34-1742">有效值</span><span class="sxs-lookup"><span data-stu-id="1da34-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1da34-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1da34-1743">apiVersion</span></span> |<span data-ttu-id="1da34-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="1da34-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="1da34-1745">要求本文</span><span class="sxs-lookup"><span data-stu-id="1da34-1745">Request Body</span></span> |<span data-ttu-id="1da34-1746">無</span><span class="sxs-lookup"><span data-stu-id="1da34-1746">NONE</span></span> |

<span data-ttu-id="1da34-1747">**回應**：</span><span class="sxs-lookup"><span data-stu-id="1da34-1747">**Response**:</span></span>

<span data-ttu-id="1da34-1748">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="1da34-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="1da34-1749">15.法律</span><span class="sxs-lookup"><span data-stu-id="1da34-1749">15. Legal</span></span>
<span data-ttu-id="1da34-1750">這份文件係依「現狀」提供。</span><span class="sxs-lookup"><span data-stu-id="1da34-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="1da34-1751">本文件中提供的資訊與畫面 (包括 URL 及其他網際網路網站參考資料) 如有變更，恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="1da34-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="1da34-1752">此處描述的一些範例僅供說明之用，純屬虛構。</span><span class="sxs-lookup"><span data-stu-id="1da34-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="1da34-1753">並未影射或關聯任何真實的人、事、物。</span><span class="sxs-lookup"><span data-stu-id="1da34-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="1da34-1754">本文件不會提供您任何法律權限 tooany 智慧財產權的任何 Microsoft 產品。</span><span class="sxs-lookup"><span data-stu-id="1da34-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="1da34-1755">您可以複製並使用這份文件，供內部參考之用。</span><span class="sxs-lookup"><span data-stu-id="1da34-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="1da34-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1da34-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="1da34-1757">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="1da34-1757">All rights reserved.</span></span>

