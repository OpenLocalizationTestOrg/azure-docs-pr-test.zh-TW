---
title: "連線到 Azure Machine Learning Web 服務 | Microsoft Docs"
description: "透過 C# 或 Python，使用授權金鑰連線到 Azure Machine Learning Web 服務。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: TRUE
ms.openlocfilehash: 0fc6c7e921b18eb14a95fb737d8fb5ab5cc7e687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-an-azure-machine-learning-web-service"></a><span data-ttu-id="397fd-103">連線到 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="397fd-103">Connect to an Azure Machine Learning Web Service</span></span>
<span data-ttu-id="397fd-104">Azure Machine Learning 開發人員體驗是一個 Web 服務 API，可即時或以批次模式從輸入資料進行預測。</span><span class="sxs-lookup"><span data-stu-id="397fd-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="397fd-105">您可以使用 Azure Machine Learning Studio 來建立預測及部署 Azure 機器學習 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="397fd-106">若要了解如何使用 Machine Learning Studio 建立和部署機器學習 Web 服務，請參閱：</span><span class="sxs-lookup"><span data-stu-id="397fd-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="397fd-107">如需如何在 Machine Learning Studio 中建立實驗的教學課程，請參閱 [建立您的第一個實驗](machine-learning-create-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="397fd-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="397fd-108">如需如何部署 Web 服務的詳細資訊，請參閱[部署 Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="397fd-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="397fd-109">如需 Machine Learning 的一般詳細資訊，請參閱 [Machine Learning 文件中心](https://azure.microsoft.com/documentation/services/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="397fd-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="397fd-110">Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="397fd-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="397fd-111">使用 Azure Machine Learning Web 服務，外部應用程式會即時與機器學習服務工作流程計分模型通訊。</span><span class="sxs-lookup"><span data-stu-id="397fd-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="397fd-112">機器學習 Web 服務呼叫會將預測結果傳回外部應用程式。</span><span class="sxs-lookup"><span data-stu-id="397fd-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="397fd-113">若要進行機器學習 Web 服務呼叫，您可以傳遞部署預測時所建立的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="397fd-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="397fd-114">機器學習服務 Web 服務以 REST 為基礎，這是一種常見的 Web 程式設計專案架構。</span><span class="sxs-lookup"><span data-stu-id="397fd-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="397fd-115">Azure Machine Learning 有兩種類型的服務：</span><span class="sxs-lookup"><span data-stu-id="397fd-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="397fd-116">要求-回應服務 (RRS) – 這是一種低延遲、調整性高的服務，針對從 Machine Learning Studio 建立和部署的無狀態模型提供介面。</span><span class="sxs-lookup"><span data-stu-id="397fd-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="397fd-117">批次執行服務 (BES) – 這是一種非同步的服務，為一批資料記錄進行計分。</span><span class="sxs-lookup"><span data-stu-id="397fd-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="397fd-118">如需 Machine Learning Web 服務的詳細資訊，請參閱[部署 Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="397fd-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="397fd-119">取得 Azure Machine Learning 授權金鑰</span><span class="sxs-lookup"><span data-stu-id="397fd-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="397fd-120">當您部署實驗時，會為 Web 服務產生 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="397fd-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="397fd-121">您可以從數個位置擷取金鑰。</span><span class="sxs-lookup"><span data-stu-id="397fd-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="397fd-122">透過 Microsoft Azure Machine Learning Web 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="397fd-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="397fd-123">登入 [Microsoft Azure Machine Learning Web 服務](https://services.azureml.net)入口網站。</span><span class="sxs-lookup"><span data-stu-id="397fd-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="397fd-124">若要擷取新 Machine Learning Web 服務的 API 金鑰︰</span><span class="sxs-lookup"><span data-stu-id="397fd-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="397fd-125">在 Azure Machine Learning Web Services 入口網站中，按一下頂端功能表上的 [Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="397fd-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="397fd-126">按一下您要擷取金鑰的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="397fd-127">在頂端功能表上，按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="397fd-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="397fd-128">複製並儲存 [主要金鑰] 。</span><span class="sxs-lookup"><span data-stu-id="397fd-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="397fd-129">若要擷取傳統 Machine Learning Web 服務的 API 金鑰︰</span><span class="sxs-lookup"><span data-stu-id="397fd-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="397fd-130">在 Azure Machine Learning Web Services 入口網站中，按一下頂端功能表上的 [傳統 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="397fd-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="397fd-131">按一下您所使用的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="397fd-132">按一下您要取得金鑰的端點。</span><span class="sxs-lookup"><span data-stu-id="397fd-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="397fd-133">在頂端功能表上，按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="397fd-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="397fd-134">複製並儲存 [主要金鑰] 。</span><span class="sxs-lookup"><span data-stu-id="397fd-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="397fd-135">傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="397fd-135">Classic Web service</span></span>
 <span data-ttu-id="397fd-136">您也可以從 Machine Learning Studio 或 Azure 傳統入口網站擷取傳統 Web 服務的金鑰。</span><span class="sxs-lookup"><span data-stu-id="397fd-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="397fd-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="397fd-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="397fd-138">在 Machine Learning Studio 中，按一下左側的 [Web 服務]  。</span><span class="sxs-lookup"><span data-stu-id="397fd-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="397fd-139">按一下某個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-139">Click a Web service.</span></span> <span data-ttu-id="397fd-140">[API 金鑰] 位於 [儀表板] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="397fd-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="397fd-141">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="397fd-141">Azure classic portal</span></span>
1. <span data-ttu-id="397fd-142">按一下左側的 [機器學習]  。</span><span class="sxs-lookup"><span data-stu-id="397fd-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="397fd-143">按一下您的 Web 服務所在的工作區。</span><span class="sxs-lookup"><span data-stu-id="397fd-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="397fd-144">按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="397fd-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="397fd-145">按一下某個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-145">Click a Web service.</span></span>
5. <span data-ttu-id="397fd-146">按一下某個端點。</span><span class="sxs-lookup"><span data-stu-id="397fd-146">Click an endpoint.</span></span> <span data-ttu-id="397fd-147">[API 金鑰] 位於右下角。</span><span class="sxs-lookup"><span data-stu-id="397fd-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="397fd-148"><a id="connect"></a>連線到機器學習 Web 服務</span><span class="sxs-lookup"><span data-stu-id="397fd-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="397fd-149">您可以使用任何支援 HTTP 要求和回應的程式設計語言，連線到機器學習 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="397fd-150">您可以從機器學習 Web 服務說明頁面檢視 C#、Python 和 R 的範例。</span><span class="sxs-lookup"><span data-stu-id="397fd-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="397fd-151">**機器學習服務 API 說明**當您部署 Web 服務時，會建立機器學習服務 API 說明。</span><span class="sxs-lookup"><span data-stu-id="397fd-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="397fd-152">請參閱 [Azure 機器學習逐步解說 - 部署 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="397fd-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="397fd-153">機器學習服務 API 說明包含有關預測 Web 服務的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="397fd-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="397fd-154">按一下您所使用的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="397fd-155">按一下您想要檢視 API 說明頁面的端點。</span><span class="sxs-lookup"><span data-stu-id="397fd-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="397fd-156">在頂端功能表上，按一下 [取用] 。</span><span class="sxs-lookup"><span data-stu-id="397fd-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="397fd-157">按一下 [要求-回應] 或 [批次執行] 端點底下的 [API 說明頁面]。</span><span class="sxs-lookup"><span data-stu-id="397fd-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="397fd-158">**檢視新 Web 服務的機器學習 API 說明**</span><span class="sxs-lookup"><span data-stu-id="397fd-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="397fd-159">在 Azure Machine Learning Web 服務入口網站中：</span><span class="sxs-lookup"><span data-stu-id="397fd-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="397fd-160">按一下頂端功能表上的 [Web 服務]  。</span><span class="sxs-lookup"><span data-stu-id="397fd-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="397fd-161">按一下您要擷取金鑰的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="397fd-162">按一下 [取用]  取得要求-回應服務和批次執行服務的 URI，以及以 C#、R 和 Python 撰寫的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="397fd-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="397fd-163">按一下 [Swagger API] 從提供的 URI，取得所呼叫 API 的 Swagger 相關文件。</span><span class="sxs-lookup"><span data-stu-id="397fd-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="397fd-164">C# 範例</span><span class="sxs-lookup"><span data-stu-id="397fd-164">C# Sample</span></span>
<span data-ttu-id="397fd-165">若要連線到機器學習 Web 服務，請使用 **HttpClient** 傳遞 ScoreData。</span><span class="sxs-lookup"><span data-stu-id="397fd-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="397fd-166">ScoreData 包含 FeatureVector，這是代表 ScoreData 的數值特徵 N 維向量。</span><span class="sxs-lookup"><span data-stu-id="397fd-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="397fd-167">您要使用 API 金鑰向機器學習服務驗證。</span><span class="sxs-lookup"><span data-stu-id="397fd-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="397fd-168">若要連線到機器學習 Web 服務，必須安裝 **Microsoft.AspNet.WebApi.Client** NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="397fd-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="397fd-169">**在 Visual Studio 中安裝 Microsoft.AspNet.WebApi.Client NuGet**</span><span class="sxs-lookup"><span data-stu-id="397fd-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="397fd-170">發佈 Download dataset from UCI: Adult 2 class dataset 的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="397fd-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="397fd-171">按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="397fd-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="397fd-172">選擇 [ **Install-package Microsoft.AspNet.WebApi.Client**]。</span><span class="sxs-lookup"><span data-stu-id="397fd-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="397fd-173">**執行程式碼範例**</span><span class="sxs-lookup"><span data-stu-id="397fd-173">**To run the code sample**</span></span>

1. <span data-ttu-id="397fd-174">發佈機器學習服務範例集合中的 "Sample 1: Download dataset from UCI: Adult 2 class dataset" 實驗。</span><span class="sxs-lookup"><span data-stu-id="397fd-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="397fd-175">使用來自 Web 服務的金鑰指派 apiKey。</span><span class="sxs-lookup"><span data-stu-id="397fd-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="397fd-176">請參閱前述的 **取得 Azure Machine Learning 授權金鑰** 。</span><span class="sxs-lookup"><span data-stu-id="397fd-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="397fd-177">使用要求 URI 指派 serviceUri。</span><span class="sxs-lookup"><span data-stu-id="397fd-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="397fd-178">Python 範例</span><span class="sxs-lookup"><span data-stu-id="397fd-178">Python Sample</span></span>
<span data-ttu-id="397fd-179">若要連線到機器學習 Web 服務，請使用 **urllib2** 程式庫傳遞 ScoreData。</span><span class="sxs-lookup"><span data-stu-id="397fd-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="397fd-180">ScoreData 包含 FeatureVector，這是代表 ScoreData 的數值特徵 N 維向量。</span><span class="sxs-lookup"><span data-stu-id="397fd-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="397fd-181">您要使用 API 金鑰向機器學習服務驗證。</span><span class="sxs-lookup"><span data-stu-id="397fd-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="397fd-182">**執行程式碼範例**</span><span class="sxs-lookup"><span data-stu-id="397fd-182">**To run the code sample**</span></span>

1. <span data-ttu-id="397fd-183">部署機器學習服務範例集合中的 "Sample 1: Download dataset from UCI: Adult 2 class dataset" 實驗。</span><span class="sxs-lookup"><span data-stu-id="397fd-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="397fd-184">使用來自 Web 服務的金鑰指派 apiKey。</span><span class="sxs-lookup"><span data-stu-id="397fd-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="397fd-185">請參閱本文章接近開始處的**取得 Azure Machine Learning 授權金鑰**。</span><span class="sxs-lookup"><span data-stu-id="397fd-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="397fd-186">使用要求 URI 指派 serviceUri。</span><span class="sxs-lookup"><span data-stu-id="397fd-186">Assign serviceUri with the Request URI.</span></span>

