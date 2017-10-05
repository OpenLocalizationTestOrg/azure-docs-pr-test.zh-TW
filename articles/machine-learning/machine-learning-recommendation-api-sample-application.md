---
title: "Machine Learning Recommendations API 中的常見作業 | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 8d8efa93e820f4a745ed93c0f4d13b2438dfa1eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a><span data-ttu-id="9b480-103">建議 API 範例應用程式逐步解說</span><span class="sxs-lookup"><span data-stu-id="9b480-103">Recommendations API Sample Application Walkthrough</span></span>
> [!NOTE]
> <span data-ttu-id="9b480-104">您應該開始使用 Recommendations API 的 Cognitive Service，而不是此版本。</span><span class="sxs-lookup"><span data-stu-id="9b480-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="9b480-105">Recommendations 的 Cognitive Service 將會取代這個服務，而所有的新特徵都會在其中進行開發。</span><span class="sxs-lookup"><span data-stu-id="9b480-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="9b480-106">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="9b480-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="9b480-107">深入了解 [移轉到新的 Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="9b480-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

## <a name="purpose"></a><span data-ttu-id="9b480-108">目的</span><span class="sxs-lookup"><span data-stu-id="9b480-108">Purpose</span></span>
<span data-ttu-id="9b480-109">本文件透過 [範例應用程式](https://code.msdn.microsoft.com/Recommendations-144df403)說明一些 Azure Machine Learning Recommendations API 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="9b480-109">This document shows the usage of the Azure Machine Learning Recommendations API via a [sample application](https://code.msdn.microsoft.com/Recommendations-144df403).</span></span>

<span data-ttu-id="9b480-110">此應用程式並非預期要包含完整的功能，也不會使用所有的 API。</span><span class="sxs-lookup"><span data-stu-id="9b480-110">This application is not intended to include full functionality, nor does it use all the APIs.</span></span> <span data-ttu-id="9b480-111">它會示範一些常見的作業，以在您第一次想要試試機器學習服務建議服務時執行。</span><span class="sxs-lookup"><span data-stu-id="9b480-111">It demonstrates some common operations to perform when you first want to play with the Machine Learning recommendation service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-to-machine-learning-recommendation-service"></a><span data-ttu-id="9b480-112">機器學習服務建議服務簡介</span><span class="sxs-lookup"><span data-stu-id="9b480-112">Introduction to Machine Learning recommendation service</span></span>
<span data-ttu-id="9b480-113">當您根據下列資料建立建議模型時，會啟用透過機器學習服務建議服務的 Recommendations：</span><span class="sxs-lookup"><span data-stu-id="9b480-113">Recommendations via the Machine Learning recommendation service are enabled when you build a recommendation model based on the following data:</span></span>

* <span data-ttu-id="9b480-114">您想要建議的項目的儲存機制，也就是類別目錄</span><span class="sxs-lookup"><span data-stu-id="9b480-114">A repository of the items you want to recommend, also known as a catalog</span></span>
* <span data-ttu-id="9b480-115">代表每一個使用者或工作階段之項目使用的資料 (這可以經由資料擷取取得，不屬於範例應用程式的一部份)</span><span class="sxs-lookup"><span data-stu-id="9b480-115">Data representing the usage of items per user or session (this can be acquired over time via data acquisition, not as part of the sample app)</span></span>

<span data-ttu-id="9b480-116">建置建議模型之後，可以使用它來根據使用者選取的一組項目 (或單一項目)，預測使用者可能會有興趣的項目。</span><span class="sxs-lookup"><span data-stu-id="9b480-116">After a recommendation model is built, you can use it to predict items that a user might be interested in, according to a set of items (or a single item) the user selects.</span></span>

<span data-ttu-id="9b480-117">若要啟用先前的案例，請在機器學習服務建議服務中執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9b480-117">To enable the previous scenario, do the following in the Machine Learning recommendation service:</span></span>

* <span data-ttu-id="9b480-118">建立模型：這是邏輯容器，會保留資料 (目錄和使用方式) 與預測模型。</span><span class="sxs-lookup"><span data-stu-id="9b480-118">Create a model: This is a logical container that holds the data (catalog and usage) and the prediction model(s).</span></span> <span data-ttu-id="9b480-119">每個模型的容器會透過建立時配置的唯一識別碼來識別。</span><span class="sxs-lookup"><span data-stu-id="9b480-119">Each model container is identified via a unique ID, which is allocated when it is created.</span></span> <span data-ttu-id="9b480-120">這個識別碼稱為模型識別碼，並且大部分的 API 都會使用它。</span><span class="sxs-lookup"><span data-stu-id="9b480-120">This ID is called the model ID, and it is used by most of the APIs.</span></span> 
* <span data-ttu-id="9b480-121">上傳至目錄：建立模型容器之後，您即可讓該容器與目錄產生關聯</span><span class="sxs-lookup"><span data-stu-id="9b480-121">Upload to catalog: When a model container is created, you can associate to it a catalog.</span></span>

<span data-ttu-id="9b480-122">**附註**：建立模型和上傳至目錄通常會在模型生命週期中執行一次。</span><span class="sxs-lookup"><span data-stu-id="9b480-122">**Note**: Creating a model and uploading to a catalog are usually performed once for the model lifecycle.</span></span>

* <span data-ttu-id="9b480-123">上傳使用狀況資料：這會將使用狀況資料加入至模型容器。</span><span class="sxs-lookup"><span data-stu-id="9b480-123">Upload usage: This adds usage data to the model container.</span></span>
* <span data-ttu-id="9b480-124">建置建議的模型：您有足夠的資料之後，您可以建置建議模型。</span><span class="sxs-lookup"><span data-stu-id="9b480-124">Build a recommendation model: After you have enough data, you can build the recommendation model.</span></span> <span data-ttu-id="9b480-125">這項作業將使用最高層機器學習演算法來建立建議模型。</span><span class="sxs-lookup"><span data-stu-id="9b480-125">This operation uses the top Machine Learning algorithms to create a recommendation model.</span></span> <span data-ttu-id="9b480-126">每個組建都與唯一識別碼相關聯。</span><span class="sxs-lookup"><span data-stu-id="9b480-126">Each build is associated with a unique ID.</span></span> <span data-ttu-id="9b480-127">您要保留這個識別碼的記錄，因為它是某些 API 的功能所需。</span><span class="sxs-lookup"><span data-stu-id="9b480-127">You need to keep a record of this ID because it is necessary for the functionality of some APIs.</span></span>
* <span data-ttu-id="9b480-128">監控建置程序：建議模型建置是一項非同步作業，視資料量 (目錄和使用) 和建置參數而定，所需的時間從數分鐘到數小時。</span><span class="sxs-lookup"><span data-stu-id="9b480-128">Monitor the building process: A recommendation model build is an asynchronous operation, and it can take from several minutes to several hours, depending on the amount of data (catalog and usage) and the build parameters.</span></span> <span data-ttu-id="9b480-129">因此，您必須監視組建。</span><span class="sxs-lookup"><span data-stu-id="9b480-129">Therefore, you need to monitor the build.</span></span> <span data-ttu-id="9b480-130">建議模型只有在與其相關聯的建置成功完成時才會建立。</span><span class="sxs-lookup"><span data-stu-id="9b480-130">A recommendation model is created only if its associated build completes successfully.</span></span>
* <span data-ttu-id="9b480-131">(選擇性) 選擇使用中建議模型建置：只有在模型容器中已建置一個以上的建議模型時，才需要執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="9b480-131">(Optional) Choose an active recommendation model build: This step is only necessary if you have more than one recommendation model built in your model container.</span></span> <span data-ttu-id="9b480-132">若未指出使用中建議模型，系統會將任何取得建議的要求自動重新導向至預設的使用中組建。</span><span class="sxs-lookup"><span data-stu-id="9b480-132">Any request to get recommendations without indicating the active recommendation model is redirected automatically by the system to the default active build.</span></span> 

<span data-ttu-id="9b480-133">**注意**：作用中的建議模型可在實際執行環境中使用，而且它是針對實際執行環境工作負載所建置。</span><span class="sxs-lookup"><span data-stu-id="9b480-133">**Note**: An active recommendation model is production ready and it is built for production workload.</span></span> <span data-ttu-id="9b480-134">這不同於非作用中建議的模型，其仍會維持在類似測試的環境中 (有時稱為「預備」)。</span><span class="sxs-lookup"><span data-stu-id="9b480-134">This differs from a non-active recommendation model, which stays in a test-like environment (sometimes called staging).</span></span>

* <span data-ttu-id="9b480-135">取得建議：具備建議模型之後，您可以針對您選取的單一項目或項目清單觸發建議。</span><span class="sxs-lookup"><span data-stu-id="9b480-135">Get recommendations: After you have a recommendation model, you can trigger recommendations for a single item or a list of items that you select.</span></span> 

<span data-ttu-id="9b480-136">您通常會在特定期間叫用「取得建議」。</span><span class="sxs-lookup"><span data-stu-id="9b480-136">You will usually invoke Get Recommendation for a certain period of time.</span></span> <span data-ttu-id="9b480-137">在該段時間，您可以將使用量資料重新導向至機器學習服務建議系統，它會將此資料加入至指定的模型容器。</span><span class="sxs-lookup"><span data-stu-id="9b480-137">During that period of time, you can redirect usage data to the Machine Learning recommendation system, which adds this data to the specified model container.</span></span> <span data-ttu-id="9b480-138">當您有足夠的使用量資料時，您可以建立新的建議模型，其中包含額外的使用量資料。</span><span class="sxs-lookup"><span data-stu-id="9b480-138">When you have enough usage data, you can build a new recommendation model that incorporates the additional usage data.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9b480-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="9b480-139">Prerequisites</span></span>
* <span data-ttu-id="9b480-140">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="9b480-140">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="9b480-141">網際網路存取</span><span class="sxs-lookup"><span data-stu-id="9b480-141">Internet access</span></span> 
* <span data-ttu-id="9b480-142">Recommendations API 的訂用帳戶 (https://datamarket.azure.com/dataset/amla/recommendations)。</span><span class="sxs-lookup"><span data-stu-id="9b480-142">Subscription to the Recommendations API (https://datamarket.azure.com/dataset/amla/recommendations).</span></span>

## <a name="azure-machine-learning-sample-app-solution"></a><span data-ttu-id="9b480-143">Azure Machine Learning 範例 App 方案</span><span class="sxs-lookup"><span data-stu-id="9b480-143">Azure Machine Learning sample app solution</span></span>
<span data-ttu-id="9b480-144">這個方案包含原始程式碼、範例使用、目錄檔案及指示詞，以下載編譯所需的套件。</span><span class="sxs-lookup"><span data-stu-id="9b480-144">This solution contains the source code, sample usage, catalog file, and directives to download the packages that are required for compilation.</span></span>

## <a name="the-apis-used"></a><span data-ttu-id="9b480-145">使用的 API</span><span class="sxs-lookup"><span data-stu-id="9b480-145">The APIs used</span></span>
<span data-ttu-id="9b480-146">應用程式會透過可用 API 的子集使用機器學習服務建議功能。</span><span class="sxs-lookup"><span data-stu-id="9b480-146">The application uses Machine Learning recommendation functionality via a subset of available APIs.</span></span> <span data-ttu-id="9b480-147">應用程式中會示範下列 API：</span><span class="sxs-lookup"><span data-stu-id="9b480-147">The following APIs are demonstrated in the application:</span></span>

* <span data-ttu-id="9b480-148">建立模型：建立邏輯容器以保存資料和建議模型。</span><span class="sxs-lookup"><span data-stu-id="9b480-148">Create model: Create a logical container to hold data and recommendation models.</span></span> <span data-ttu-id="9b480-149">模型是以名稱識別，而您無法建立同名的模型超過一次。</span><span class="sxs-lookup"><span data-stu-id="9b480-149">A model is identified by a name, and you  cannot create more than one model with the same name.</span></span>
* <span data-ttu-id="9b480-150">上傳目錄檔案：用來上傳目錄資料。</span><span class="sxs-lookup"><span data-stu-id="9b480-150">Upload catalog file: Use to upload catalog data.</span></span>
* <span data-ttu-id="9b480-151">上傳使用檔案：用來上傳使用資料。</span><span class="sxs-lookup"><span data-stu-id="9b480-151">Upload usage file: Use to upload usage data.</span></span>
* <span data-ttu-id="9b480-152">觸發建置：用來建立建議模型。</span><span class="sxs-lookup"><span data-stu-id="9b480-152">Trigger build: Use to create a recommendation model.</span></span>
* <span data-ttu-id="9b480-153">監視組建執行：用來監視建議模型組建的狀態</span><span class="sxs-lookup"><span data-stu-id="9b480-153">Monitor build execution: Use to monitor the status of a recommendation model build.</span></span>
* <span data-ttu-id="9b480-154">選擇建議的建置模型：用來指出特定模型容器預設要使用的建議模型。</span><span class="sxs-lookup"><span data-stu-id="9b480-154">Choose a built model for recommendation: Use to indicate which recommendation model to use by default for a certain model container.</span></span> <span data-ttu-id="9b480-155">只有在您有一個以上的建議模型，而且想要啟動非使用中組建作為使用中建議時，才需要執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="9b480-155">This step is necessary only if you have more than one recommendation model and you want to activate a non-active build as the active recommendation model.</span></span>
* <span data-ttu-id="9b480-156">取得建議：用來根據指定的單一項目或一組項目擷取建議項目。</span><span class="sxs-lookup"><span data-stu-id="9b480-156">Get recommendation: Use to retrieve recommended items according to a given single item or a set of items.</span></span> 

<span data-ttu-id="9b480-157">如需 API 的完整描述，請參閱 Microsoft Azure Marketplace 文件。</span><span class="sxs-lookup"><span data-stu-id="9b480-157">For a complete description of the APIs, please see the Microsoft Azure Marketplace documentation.</span></span> 

<span data-ttu-id="9b480-158">**附註**：一個模型經過一段時間 (非同時) 可以有數個組建。</span><span class="sxs-lookup"><span data-stu-id="9b480-158">**Note**: A model can have several builds over time (not simultaneously).</span></span> <span data-ttu-id="9b480-159">每個組建會使用相同或更新的目錄和其他使用量資料建立。</span><span class="sxs-lookup"><span data-stu-id="9b480-159">Each build is created with the same or an updated catalog and additional usage data.</span></span>

## <a name="common-pitfalls"></a><span data-ttu-id="9b480-160">常見陷阱</span><span class="sxs-lookup"><span data-stu-id="9b480-160">Common pitfalls</span></span>
* <span data-ttu-id="9b480-161">您必須提供您的使用者名稱和您的 Microsoft Azure Marketplace 主要帳戶金鑰來執行範例 App。</span><span class="sxs-lookup"><span data-stu-id="9b480-161">You need to provide your user name and your Microsoft Azure Marketplace primary account key to run the sample app.</span></span>
* <span data-ttu-id="9b480-162">連續執行範例應用程式將會失敗。</span><span class="sxs-lookup"><span data-stu-id="9b480-162">Running the sample app consecutively will fail.</span></span> <span data-ttu-id="9b480-163">應用程式流程可能包括從預先定義之模型建立、上傳、建置監視器及取得建議，因此如果您未在引動之間變更模型名稱，它就無法連續執行。</span><span class="sxs-lookup"><span data-stu-id="9b480-163">The application flow includes creating, uploading, building the monitor, and getting recommendations from a predefined model; therefore, it will fail on consecutive execution if you do not change the model name between invocations.</span></span>
* <span data-ttu-id="9b480-164">Recommendations 可能不會傳回任何資料。</span><span class="sxs-lookup"><span data-stu-id="9b480-164">Recommendations might return without data.</span></span> <span data-ttu-id="9b480-165">範例應用程式會使用非常小的目錄和使用方式檔案。</span><span class="sxs-lookup"><span data-stu-id="9b480-165">The sample app uses a very small catalog and usage file.</span></span> <span data-ttu-id="9b480-166">因此，類別目錄中的某些項目將不會有任何建議的項目。</span><span class="sxs-lookup"><span data-stu-id="9b480-166">Therefore, some items from the catalog will have no recommended items.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="9b480-167">免責聲明</span><span class="sxs-lookup"><span data-stu-id="9b480-167">Disclaimer</span></span>
<span data-ttu-id="9b480-168">範例應用程式並非預期在實際執行環境中執行。</span><span class="sxs-lookup"><span data-stu-id="9b480-168">The sample app is not intended to be run in a production environment.</span></span> <span data-ttu-id="9b480-169">目錄中提供的資料太小，而且它將不會提供有意義的建議模型。</span><span class="sxs-lookup"><span data-stu-id="9b480-169">The data provided in the catalog is very small, and it will not provide a meaningful recommendation model.</span></span> <span data-ttu-id="9b480-170">提供資料基於示範目的。</span><span class="sxs-lookup"><span data-stu-id="9b480-170">The data is provided as a demonstration.</span></span> 

