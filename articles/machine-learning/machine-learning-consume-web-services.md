---
title: "aaaHow tooconsume Azure 機器學習 Web 服務 |Microsoft 文件"
description: "機器學習服務部署之後，就可以取用 hello RESTFul Web 服務所提供的即時要求-回應服務，或是以批次執行服務。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 19095604169e5af1daed12c17ba66258233178bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconsume-an-azure-machine-learning-web-service"></a><span data-ttu-id="363d0-103">如何 tooconsume Azure 機器學習 Web 服務</span><span class="sxs-lookup"><span data-stu-id="363d0-103">How tooconsume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="363d0-104">一旦您部署為 Web 服務的 Azure Machine Learning 預測模型，您可以使用 REST API toosend 它的資料，以及如何取得預測。</span><span class="sxs-lookup"><span data-stu-id="363d0-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API toosend it data and get predictions.</span></span> <span data-ttu-id="363d0-105">在即時或批次模式中，您可以傳送 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="363d0-105">You can send hello data in real-time or in batch mode.</span></span>

<span data-ttu-id="363d0-106">您可以找到更多有關 toocreate 及部署機器學習 Web 服務，使用此處 Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="363d0-106">You can find more information about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="363d0-107">如需如何 toocreate 實驗在機器學習 Studio 中，請參閱教學課程[建立第一個實驗](machine-learning-create-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="363d0-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="363d0-108">如需詳細資訊，如何 toodeploy Web 服務，請參閱[部署機器學習 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="363d0-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="363d0-109">如需機器學習一般情況下，請瀏覽 hello[機器學習服務文件中心](https://azure.microsoft.com/documentation/services/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="363d0-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="363d0-110">概觀</span><span class="sxs-lookup"><span data-stu-id="363d0-110">Overview</span></span>
<span data-ttu-id="363d0-111">Hello Azure 機器學習 Web 服務，與外部應用程式與即時的機器學習服務工作流程計分模型進行通訊。</span><span class="sxs-lookup"><span data-stu-id="363d0-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="363d0-112">在機器學習 Web 服務呼叫傳回預測結果 tooan 外部應用程式。</span><span class="sxs-lookup"><span data-stu-id="363d0-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="363d0-113">toomake 在機器學習 Web 服務呼叫，您將部署預測時，會建立 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="363d0-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="363d0-114">hello 機器學習 Web 服務根據其餘部分，web 程式設計專案常用的架構選項。</span><span class="sxs-lookup"><span data-stu-id="363d0-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="363d0-115">Azure Machine Learning 有兩種類型的服務：</span><span class="sxs-lookup"><span data-stu-id="363d0-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="363d0-116">要求-回應服務 (RR)-低延遲、 高擴充性服務 toohello 無狀態模型建立和部署的 hello Machine Learning Studio 提供的介面。</span><span class="sxs-lookup"><span data-stu-id="363d0-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="363d0-117">批次執行服務 (BES) – 這是一種非同步的服務，為一批資料記錄進行計分。</span><span class="sxs-lookup"><span data-stu-id="363d0-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="363d0-118">如需 Machine Learning Web 服務的詳細資訊，請參閱[部署 Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="363d0-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="363d0-119">取得 Azure Machine Learning 授權金鑰</span><span class="sxs-lookup"><span data-stu-id="363d0-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="363d0-120">當您部署您的經驗時，會產生 API 金鑰 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="363d0-121">您可以從數個位置擷取 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="363d0-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="363d0-122">從 hello Microsoft Azure 機器學習 Web 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="363d0-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="363d0-123">登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net)入口網站。</span><span class="sxs-lookup"><span data-stu-id="363d0-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="363d0-124">新的機器學習 Web 服務的 tooretrieve hello API 金鑰：</span><span class="sxs-lookup"><span data-stu-id="363d0-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="363d0-125">在 hello Azure 機器學習 Web 服務入口網站中，按一下  **Web 服務**hello 上方的功能表。</span><span class="sxs-lookup"><span data-stu-id="363d0-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="363d0-126">按一下您想要的 tooretrieve hello 金鑰 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="363d0-127">在 hello 上方功能表中，按一下 **取用**。</span><span class="sxs-lookup"><span data-stu-id="363d0-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="363d0-128">複製並儲存 hello**主索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="363d0-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="363d0-129">傳統的機器學習 Web 服務的 tooretrieve hello API 金鑰：</span><span class="sxs-lookup"><span data-stu-id="363d0-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="363d0-130">在 hello Azure 機器學習 Web 服務入口網站中，按一下 **傳統 Web 服務**hello 上方的功能表。</span><span class="sxs-lookup"><span data-stu-id="363d0-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="363d0-131">按一下您要使用的 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="363d0-132">按一下您想要的 tooretrieve hello 金鑰 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="363d0-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="363d0-133">在 hello 上方功能表中，按一下 **取用**。</span><span class="sxs-lookup"><span data-stu-id="363d0-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="363d0-134">複製並儲存 hello**主索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="363d0-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="363d0-135">傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="363d0-135">Classic Web service</span></span>
 <span data-ttu-id="363d0-136">您也可以擷取從 Machine Learning Studio 或 hello Azure 傳統入口網站的傳統 Web 服務的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="363d0-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="363d0-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="363d0-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="363d0-138">在機器學習 Studio 中，按一下  **WEB 服務**hello 左側。</span><span class="sxs-lookup"><span data-stu-id="363d0-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="363d0-139">按一下某個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-139">Click a Web service.</span></span> <span data-ttu-id="363d0-140">hello **API 金鑰**位於 hello**儀表板** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="363d0-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="363d0-141">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="363d0-141">Azure classic portal</span></span>
1. <span data-ttu-id="363d0-142">按一下**MACHINE LEARNING** hello 左側。</span><span class="sxs-lookup"><span data-stu-id="363d0-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="363d0-143">按一下您的 Web 服務所在的 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="363d0-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="363d0-144">按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="363d0-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="363d0-145">按一下某個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-145">Click a Web service.</span></span>
5. <span data-ttu-id="363d0-146">按一下某個端點。</span><span class="sxs-lookup"><span data-stu-id="363d0-146">Click an endpoint.</span></span> <span data-ttu-id="363d0-147">hello 「 API 金鑰 」 已關閉在 hello 右下方。</span><span class="sxs-lookup"><span data-stu-id="363d0-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="363d0-148"><a id="connect"></a>Tooa 機器學習 Web 服務連接</span><span class="sxs-lookup"><span data-stu-id="363d0-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="363d0-149">您可以連接 tooa 使用任何支援 HTTP 要求和回應的程式設計語言的機器學習 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="363d0-150">您可以從機器學習 Web 服務說明頁面檢視 C#、Python 和 R 的範例。</span><span class="sxs-lookup"><span data-stu-id="363d0-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="363d0-151">**機器學習服務 API 說明**當您部署 Web 服務時，會建立機器學習服務 API 說明。</span><span class="sxs-lookup"><span data-stu-id="363d0-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="363d0-152">請參閱 [Azure 機器學習逐步解說 - 部署 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="363d0-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="363d0-153">hello 機器學習 API 說明包含預測 Web 服務的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="363d0-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="363d0-154">按一下您要使用的 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="363d0-155">按一下您想要的 tooview hello API 說明頁面的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="363d0-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="363d0-156">在 hello 上方功能表中，按一下 **取用**。</span><span class="sxs-lookup"><span data-stu-id="363d0-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="363d0-157">按一下**API 說明頁面**hello 要求-回應] 或 [批次執行端點之下。</span><span class="sxs-lookup"><span data-stu-id="363d0-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="363d0-158">**tooview 機器學習 API 說明新的 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="363d0-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="363d0-159">在 hello Azure 機器學習 Web 服務入口網站：</span><span class="sxs-lookup"><span data-stu-id="363d0-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="363d0-160">按一下**WEB 服務**hello 上方功能表上。</span><span class="sxs-lookup"><span data-stu-id="363d0-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="363d0-161">按一下您想要的 tooretrieve hello 金鑰 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="363d0-162">按一下**取用**tooget hello hello 要求 Reposonse 與 C#、 R 和 Python 中的批次執行服務和範例程式碼的 Uri。</span><span class="sxs-lookup"><span data-stu-id="363d0-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="363d0-163">按一下**Swagger API** tooget Swagger 根據文件 hello 應用程式開發介面呼叫 hello 從提供的 Uri。</span><span class="sxs-lookup"><span data-stu-id="363d0-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="363d0-164">C# 範例</span><span class="sxs-lookup"><span data-stu-id="363d0-164">C# Sample</span></span>
<span data-ttu-id="363d0-165">tooconnect tooa 機器學習 Web 服務，使用**HttpClient**傳遞 ScoreData。</span><span class="sxs-lookup"><span data-stu-id="363d0-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="363d0-166">ScoreData 包含 FeatureVector，代表 hello ScoreData n 維向量的數字的功能。</span><span class="sxs-lookup"><span data-stu-id="363d0-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="363d0-167">您 API 金鑰與驗證 toohello 機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="363d0-168">tooconnect tooa 機器學習 Web 服務，hello **Microsoft.AspNet.WebApi.Client**必須安裝 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="363d0-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="363d0-169">**在 Visual Studio 中安裝 Microsoft.AspNet.WebApi.Client NuGet**</span><span class="sxs-lookup"><span data-stu-id="363d0-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="363d0-170">發行 hello 下載 UCI 資料集： 成人 2 類別的資料集 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="363d0-171">按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="363d0-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="363d0-172">選擇 [ **Install-package Microsoft.AspNet.WebApi.Client**]。</span><span class="sxs-lookup"><span data-stu-id="363d0-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="363d0-173">**toorun hello 程式碼範例**</span><span class="sxs-lookup"><span data-stu-id="363d0-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="363d0-174">發行 」 範例 1： 下載 UCI 資料集： 成人 2 類別的資料集 」 實驗、 hello 機器學習範例集合的一部分。</span><span class="sxs-lookup"><span data-stu-id="363d0-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="363d0-175">指派 apiKey 與 hello 索引鍵，從 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="363d0-176">請參閱前述的 **取得 Azure Machine Learning 授權金鑰** 。</span><span class="sxs-lookup"><span data-stu-id="363d0-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="363d0-177">指派 serviceUri 以 hello 要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="363d0-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="363d0-178">Python 範例</span><span class="sxs-lookup"><span data-stu-id="363d0-178">Python Sample</span></span>
<span data-ttu-id="363d0-179">tooconnect tooa 機器學習 Web 服務，使用 hello **urllib2**傳遞 ScoreData 程式庫。</span><span class="sxs-lookup"><span data-stu-id="363d0-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="363d0-180">ScoreData 包含 FeatureVector，代表 hello ScoreData n 維向量的數字的功能。</span><span class="sxs-lookup"><span data-stu-id="363d0-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="363d0-181">您 API 金鑰與驗證 toohello 機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="363d0-182">**toorun hello 程式碼範例**</span><span class="sxs-lookup"><span data-stu-id="363d0-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="363d0-183">部署 」 範例 1： 下載 UCI 資料集： 成人 2 類別的資料集 」 實驗、 hello 機器學習範例集合的一部分。</span><span class="sxs-lookup"><span data-stu-id="363d0-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="363d0-184">指派 apiKey 與 hello 索引鍵，從 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="363d0-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="363d0-185">請參閱 hello**取得 Azure Machine Learning 授權金鑰**hello 開頭附近的這篇文章的一節。</span><span class="sxs-lookup"><span data-stu-id="363d0-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="363d0-186">指派 serviceUri 以 hello 要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="363d0-186">Assign serviceUri with hello Request URI.</span></span>

