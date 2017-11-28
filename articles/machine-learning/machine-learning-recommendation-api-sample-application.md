---
title: "aaaCommon hello 機器學習建議 API 中的作業 |Microsoft 文件"
description: "Azure ML Recommendation 範例應用程式"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
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
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a><span data-ttu-id="d78ce-103">建議 API 範例應用程式逐步解說</span><span class="sxs-lookup"><span data-stu-id="d78ce-103">Recommendations API Sample Application Walkthrough</span></span>
> [!NOTE]
> <span data-ttu-id="d78ce-104">您應該開始使用 hello 建議 API 認知服務，而不此版本。</span><span class="sxs-lookup"><span data-stu-id="d78ce-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="d78ce-105">hello 建議認知服務將會取代此服務，並將那里開發所有 hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="d78ce-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="d78ce-106">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="d78ce-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="d78ce-107">深入了解[移轉 toohello 新認知的服務](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="d78ce-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

## <a name="purpose"></a><span data-ttu-id="d78ce-108">目的</span><span class="sxs-lookup"><span data-stu-id="d78ce-108">Purpose</span></span>
<span data-ttu-id="d78ce-109">本文件說明的 hello hello 使用量透過的 Azure 機器學習建議 API[範例應用程式](https://code.msdn.microsoft.com/Recommendations-144df403)。</span><span class="sxs-lookup"><span data-stu-id="d78ce-109">This document shows hello usage of hello Azure Machine Learning Recommendations API via a [sample application](https://code.msdn.microsoft.com/Recommendations-144df403).</span></span>

<span data-ttu-id="d78ce-110">此應用程式不屬於預期的 tooinclude 完整功能，也不會使用所有 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="d78ce-110">This application is not intended tooinclude full functionality, nor does it use all hello APIs.</span></span> <span data-ttu-id="d78ce-111">當您第一次想 tooplay 以 hello Machine Learning 建議服務時，它會示範一些常見的作業 tooperform。</span><span class="sxs-lookup"><span data-stu-id="d78ce-111">It demonstrates some common operations tooperform when you first want tooplay with hello Machine Learning recommendation service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a><span data-ttu-id="d78ce-112">簡介 tooMachine 學習建議服務</span><span class="sxs-lookup"><span data-stu-id="d78ce-112">Introduction tooMachine Learning recommendation service</span></span>
<span data-ttu-id="d78ce-113">當您建置 hello 下列資料為基礎的建議模型時，會啟用建議透過 hello Machine Learning 建議服務：</span><span class="sxs-lookup"><span data-stu-id="d78ce-113">Recommendations via hello Machine Learning recommendation service are enabled when you build a recommendation model based on hello following data:</span></span>

* <span data-ttu-id="d78ce-114">您想要的 toorecommend，也就是為類別目錄的 hello 項目儲存機制</span><span class="sxs-lookup"><span data-stu-id="d78ce-114">A repository of hello items you want toorecommend, also known as a catalog</span></span>
* <span data-ttu-id="d78ce-115">代表 hello 的項目，每個使用者或工作階段 （這可以取得一段時間，透過資料擷取，不 hello 範例應用程式的一部分） 的使用方式資料</span><span class="sxs-lookup"><span data-stu-id="d78ce-115">Data representing hello usage of items per user or session (this can be acquired over time via data acquisition, not as part of hello sample app)</span></span>

<span data-ttu-id="d78ce-116">建立建議模型之後，您可以使用它 toopredict 項目，使用者可能感興趣，根據 tooa 組項目 （或單一項目） hello 使用者選取。</span><span class="sxs-lookup"><span data-stu-id="d78ce-116">After a recommendation model is built, you can use it toopredict items that a user might be interested in, according tooa set of items (or a single item) hello user selects.</span></span>

<span data-ttu-id="d78ce-117">tooenable hello 前述案例中，執行中的 hello 下列 hello Machine Learning 建議服務：</span><span class="sxs-lookup"><span data-stu-id="d78ce-117">tooenable hello previous scenario, do hello following in hello Machine Learning recommendation service:</span></span>

* <span data-ttu-id="d78ce-118">建立模型： 這是保留 hello 資料 （目錄和使用方式） 和 hello 預測模型的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="d78ce-118">Create a model: This is a logical container that holds hello data (catalog and usage) and hello prediction model(s).</span></span> <span data-ttu-id="d78ce-119">每個模型的容器會透過建立時配置的唯一識別碼來識別。</span><span class="sxs-lookup"><span data-stu-id="d78ce-119">Each model container is identified via a unique ID, which is allocated when it is created.</span></span> <span data-ttu-id="d78ce-120">此識別碼稱為 hello 模型識別碼，和大部分的 hello 應用程式開發介面使用它。</span><span class="sxs-lookup"><span data-stu-id="d78ce-120">This ID is called hello model ID, and it is used by most of hello APIs.</span></span> 
* <span data-ttu-id="d78ce-121">上傳 toocatalog： 建立模型容器時，您可以將關聯 tooit 類別目錄。</span><span class="sxs-lookup"><span data-stu-id="d78ce-121">Upload toocatalog: When a model container is created, you can associate tooit a catalog.</span></span>

<span data-ttu-id="d78ce-122">**請注意**： 建立模型及上傳 tooa 目錄通常就會執行一次 hello 模型的生命週期。</span><span class="sxs-lookup"><span data-stu-id="d78ce-122">**Note**: Creating a model and uploading tooa catalog are usually performed once for hello model lifecycle.</span></span>

* <span data-ttu-id="d78ce-123">上傳使用方式： 這會將使用量資料 toohello 模型容器。</span><span class="sxs-lookup"><span data-stu-id="d78ce-123">Upload usage: This adds usage data toohello model container.</span></span>
* <span data-ttu-id="d78ce-124">建立建議模型： 您擁有足夠的資料之後，您可以建立 hello 推薦模型。</span><span class="sxs-lookup"><span data-stu-id="d78ce-124">Build a recommendation model: After you have enough data, you can build hello recommendation model.</span></span> <span data-ttu-id="d78ce-125">這項作業會使用最上層機器學習演算法 toocreate hello 推薦模型。</span><span class="sxs-lookup"><span data-stu-id="d78ce-125">This operation uses hello top Machine Learning algorithms toocreate a recommendation model.</span></span> <span data-ttu-id="d78ce-126">每個組建都與唯一識別碼相關聯。</span><span class="sxs-lookup"><span data-stu-id="d78ce-126">Each build is associated with a unique ID.</span></span> <span data-ttu-id="d78ce-127">您需要 tookeep 此識別碼的記錄，因為它為某些應用程式開發介面的 hello 功能所需。</span><span class="sxs-lookup"><span data-stu-id="d78ce-127">You need tookeep a record of this ID because it is necessary for hello functionality of some APIs.</span></span>
* <span data-ttu-id="d78ce-128">建立處理序監視器 hello： 建議模型建置是非同步作業，它可以和花幾分鐘 tooseveral 小時，視 hello （類別目錄和使用方式） 的資料數量而定 hello 組建參數。</span><span class="sxs-lookup"><span data-stu-id="d78ce-128">Monitor hello building process: A recommendation model build is an asynchronous operation, and it can take from several minutes tooseveral hours, depending on hello amount of data (catalog and usage) and hello build parameters.</span></span> <span data-ttu-id="d78ce-129">因此，您需要 toomonitor hello 組建。</span><span class="sxs-lookup"><span data-stu-id="d78ce-129">Therefore, you need toomonitor hello build.</span></span> <span data-ttu-id="d78ce-130">建議模型只有在與其相關聯的建置成功完成時才會建立。</span><span class="sxs-lookup"><span data-stu-id="d78ce-130">A recommendation model is created only if its associated build completes successfully.</span></span>
* <span data-ttu-id="d78ce-131">(選擇性) 選擇使用中建議模型建置：只有在模型容器中已建置一個以上的建議模型時，才需要執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="d78ce-131">(Optional) Choose an active recommendation model build: This step is only necessary if you have more than one recommendation model built in your model container.</span></span> <span data-ttu-id="d78ce-132">指出 hello 作用中的建議模型沒有任何要求 tooget 建議是由 hello 系統 toohello 預設作用中建置自動重新導向。</span><span class="sxs-lookup"><span data-stu-id="d78ce-132">Any request tooget recommendations without indicating hello active recommendation model is redirected automatically by hello system toohello default active build.</span></span> 

<span data-ttu-id="d78ce-133">**注意**：作用中的建議模型可在實際執行環境中使用，而且它是針對實際執行環境工作負載所建置。</span><span class="sxs-lookup"><span data-stu-id="d78ce-133">**Note**: An active recommendation model is production ready and it is built for production workload.</span></span> <span data-ttu-id="d78ce-134">這不同於非作用中建議的模型，其仍會維持在類似測試的環境中 (有時稱為「預備」)。</span><span class="sxs-lookup"><span data-stu-id="d78ce-134">This differs from a non-active recommendation model, which stays in a test-like environment (sometimes called staging).</span></span>

* <span data-ttu-id="d78ce-135">取得建議：具備建議模型之後，您可以針對您選取的單一項目或項目清單觸發建議。</span><span class="sxs-lookup"><span data-stu-id="d78ce-135">Get recommendations: After you have a recommendation model, you can trigger recommendations for a single item or a list of items that you select.</span></span> 

<span data-ttu-id="d78ce-136">您通常會在特定期間叫用「取得建議」。</span><span class="sxs-lookup"><span data-stu-id="d78ce-136">You will usually invoke Get Recommendation for a certain period of time.</span></span> <span data-ttu-id="d78ce-137">在這段時間，您可以重新導向使用方式資料 toohello Machine Learning 建議系統，這會將此資料 toohello 指定之模型的容器。</span><span class="sxs-lookup"><span data-stu-id="d78ce-137">During that period of time, you can redirect usage data toohello Machine Learning recommendation system, which adds this data toohello specified model container.</span></span> <span data-ttu-id="d78ce-138">當您有足夠的使用方式資料時，您可以建立新的建議模型，其中包含 hello 其他使用量資料。</span><span class="sxs-lookup"><span data-stu-id="d78ce-138">When you have enough usage data, you can build a new recommendation model that incorporates hello additional usage data.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d78ce-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="d78ce-139">Prerequisites</span></span>
* <span data-ttu-id="d78ce-140">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="d78ce-140">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="d78ce-141">網際網路存取</span><span class="sxs-lookup"><span data-stu-id="d78ce-141">Internet access</span></span> 
* <span data-ttu-id="d78ce-142">訂用帳戶 toohello 建議應用程式開發介面 (https://datamarket.azure.com/dataset/amla/recommendations)。</span><span class="sxs-lookup"><span data-stu-id="d78ce-142">Subscription toohello Recommendations API (https://datamarket.azure.com/dataset/amla/recommendations).</span></span>

## <a name="azure-machine-learning-sample-app-solution"></a><span data-ttu-id="d78ce-143">Azure Machine Learning 範例 App 方案</span><span class="sxs-lookup"><span data-stu-id="d78ce-143">Azure Machine Learning sample app solution</span></span>
<span data-ttu-id="d78ce-144">此方案包含 hello 來源程式碼、 範例使用方式、 類別目錄檔案和指示詞 toodownload hello 封裝所需的編譯。</span><span class="sxs-lookup"><span data-stu-id="d78ce-144">This solution contains hello source code, sample usage, catalog file, and directives toodownload hello packages that are required for compilation.</span></span>

## <a name="hello-apis-used"></a><span data-ttu-id="d78ce-145">hello 使用的應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="d78ce-145">hello APIs used</span></span>
<span data-ttu-id="d78ce-146">hello 應用程式會使用機器學習建議功能，透過可用的應用程式開發介面的子集。</span><span class="sxs-lookup"><span data-stu-id="d78ce-146">hello application uses Machine Learning recommendation functionality via a subset of available APIs.</span></span> <span data-ttu-id="d78ce-147">hello hello 應用程式將示範下列 Api:</span><span class="sxs-lookup"><span data-stu-id="d78ce-147">hello following APIs are demonstrated in hello application:</span></span>

* <span data-ttu-id="d78ce-148">建立模型： 建立邏輯容器 toohold 資料和建議的模型。</span><span class="sxs-lookup"><span data-stu-id="d78ce-148">Create model: Create a logical container toohold data and recommendation models.</span></span> <span data-ttu-id="d78ce-149">由名稱、 識別模型，而且您無法建立多個模型以 hello 相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="d78ce-149">A model is identified by a name, and you  cannot create more than one model with hello same name.</span></span>
* <span data-ttu-id="d78ce-150">類別目錄檔案上傳： 使用 tooupload 目錄資料。</span><span class="sxs-lookup"><span data-stu-id="d78ce-150">Upload catalog file: Use tooupload catalog data.</span></span>
* <span data-ttu-id="d78ce-151">使用檔案上傳： 使用 tooupload 使用方式資料。</span><span class="sxs-lookup"><span data-stu-id="d78ce-151">Upload usage file: Use tooupload usage data.</span></span>
* <span data-ttu-id="d78ce-152">觸發建置： 使用 toocreate 推薦模型。</span><span class="sxs-lookup"><span data-stu-id="d78ce-152">Trigger build: Use toocreate a recommendation model.</span></span>
* <span data-ttu-id="d78ce-153">監視組建執行： 使用推薦模型建置 toomonitor hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="d78ce-153">Monitor build execution: Use toomonitor hello status of a recommendation model build.</span></span>
* <span data-ttu-id="d78ce-154">選擇建議的內建的模型： 預設會使用 tooindicate 的建議模型 toouse 特定模型的容器。</span><span class="sxs-lookup"><span data-stu-id="d78ce-154">Choose a built model for recommendation: Use tooindicate which recommendation model toouse by default for a certain model container.</span></span> <span data-ttu-id="d78ce-155">您有一個以上的建議模型，而且您想的 tooactivate 非作用中建置為 hello 作用中的建議模型時，才需要此步驟。</span><span class="sxs-lookup"><span data-stu-id="d78ce-155">This step is necessary only if you have more than one recommendation model and you want tooactivate a non-active build as hello active recommendation model.</span></span>
* <span data-ttu-id="d78ce-156">取得建議： 使用 tooretrieve 建議項目，根據 tooa 給定的單一項目或一組項目。</span><span class="sxs-lookup"><span data-stu-id="d78ce-156">Get recommendation: Use tooretrieve recommended items according tooa given single item or a set of items.</span></span> 

<span data-ttu-id="d78ce-157">Hello 應用程式開發介面的完整說明，請參閱 hello Microsoft Azure Marketplace 文件。</span><span class="sxs-lookup"><span data-stu-id="d78ce-157">For a complete description of hello APIs, please see hello Microsoft Azure Marketplace documentation.</span></span> 

<span data-ttu-id="d78ce-158">**附註**：一個模型經過一段時間 (非同時) 可以有數個組建。</span><span class="sxs-lookup"><span data-stu-id="d78ce-158">**Note**: A model can have several builds over time (not simultaneously).</span></span> <span data-ttu-id="d78ce-159">每個組建建立 hello 與相同或更新類別目錄和其他使用量資料。</span><span class="sxs-lookup"><span data-stu-id="d78ce-159">Each build is created with hello same or an updated catalog and additional usage data.</span></span>

## <a name="common-pitfalls"></a><span data-ttu-id="d78ce-160">常見陷阱</span><span class="sxs-lookup"><span data-stu-id="d78ce-160">Common pitfalls</span></span>
* <span data-ttu-id="d78ce-161">您的使用者名稱和您 Microsoft Azure Marketplace 主要帳戶金鑰 toorun hello 範例應用程式，您會需要 tooprovide。</span><span class="sxs-lookup"><span data-stu-id="d78ce-161">You need tooprovide your user name and your Microsoft Azure Marketplace primary account key toorun hello sample app.</span></span>
* <span data-ttu-id="d78ce-162">Hello 範例應用程式執行連續將會失敗。</span><span class="sxs-lookup"><span data-stu-id="d78ce-162">Running hello sample app consecutively will fail.</span></span> <span data-ttu-id="d78ce-163">hello 應用程式流程包括建立、 上傳、 建立 hello 監視器和從預先定義的模型，取得建議因此，它將無法在連續執行如果您不要變更 hello 引動過程之間的模型名稱。</span><span class="sxs-lookup"><span data-stu-id="d78ce-163">hello application flow includes creating, uploading, building hello monitor, and getting recommendations from a predefined model; therefore, it will fail on consecutive execution if you do not change hello model name between invocations.</span></span>
* <span data-ttu-id="d78ce-164">Recommendations 可能不會傳回任何資料。</span><span class="sxs-lookup"><span data-stu-id="d78ce-164">Recommendations might return without data.</span></span> <span data-ttu-id="d78ce-165">hello 範例應用程式會使用非常小的目錄和使用方式檔案。</span><span class="sxs-lookup"><span data-stu-id="d78ce-165">hello sample app uses a very small catalog and usage file.</span></span> <span data-ttu-id="d78ce-166">因此，從 hello 類別目錄的某些項目會有任何建議的項目。</span><span class="sxs-lookup"><span data-stu-id="d78ce-166">Therefore, some items from hello catalog will have no recommended items.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="d78ce-167">免責聲明</span><span class="sxs-lookup"><span data-stu-id="d78ce-167">Disclaimer</span></span>
<span data-ttu-id="d78ce-168">hello 範例應用程式不會在實際執行環境中執行的預定的 toobe。</span><span class="sxs-lookup"><span data-stu-id="d78ce-168">hello sample app is not intended toobe run in a production environment.</span></span> <span data-ttu-id="d78ce-169">hello 目錄中提供的 hello 資料太小，而且它將不會提供有意義的推薦模型。</span><span class="sxs-lookup"><span data-stu-id="d78ce-169">hello data provided in hello catalog is very small, and it will not provide a meaningful recommendation model.</span></span> <span data-ttu-id="d78ce-170">提供示範 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d78ce-170">hello data is provided as a demonstration.</span></span> 

