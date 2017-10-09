---
title: "aaaConnect tooa Machine Learning Web 服務 |Microsoft 文件"
description: "使用 C# 或 Python，連線 tooan Azure 機器學習 Web 服務使用的授權金鑰。"
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
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a><span data-ttu-id="a6c50-103">連接 tooan Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="a6c50-103">Connect tooan Azure Machine Learning Web Service</span></span>
<span data-ttu-id="a6c50-104">hello Azure Machine Learning 開發人員經驗是 Web 服務 API toomake 預測從即時或批次模式的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="a6c50-104">hello Azure Machine Learning developer experience is a Web service API toomake predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="a6c50-105">您使用 Azure Machine Learning Studio toocreate 預測，並部署 Azure 機器學習 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-105">You use Azure Machine Learning Studio toocreate predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="a6c50-106">有關如何 toolearn toocreate 及部署機器學習 Web 服務使用 Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="a6c50-106">toolearn about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="a6c50-107">如需如何 toocreate 實驗在機器學習 Studio 中，請參閱教學課程[建立第一個實驗](machine-learning-create-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="a6c50-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="a6c50-108">如需詳細資訊，如何 toodeploy Web 服務，請參閱[部署機器學習 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="a6c50-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="a6c50-109">如需機器學習一般情況下，請瀏覽 hello[機器學習服務文件中心](https://azure.microsoft.com/documentation/services/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="a6c50-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="a6c50-110">Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="a6c50-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="a6c50-111">Hello Azure 機器學習 Web 服務，與外部應用程式與即時的機器學習服務工作流程計分模型進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a6c50-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="a6c50-112">在機器學習 Web 服務呼叫傳回預測結果 tooan 外部應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6c50-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="a6c50-113">toomake 在機器學習 Web 服務呼叫，您將部署預測時，會建立 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6c50-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="a6c50-114">hello 機器學習 Web 服務根據其餘部分，web 程式設計專案常用的架構選項。</span><span class="sxs-lookup"><span data-stu-id="a6c50-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="a6c50-115">Azure Machine Learning 有兩種類型的服務：</span><span class="sxs-lookup"><span data-stu-id="a6c50-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="a6c50-116">要求-回應服務 (RR)-低延遲、 高擴充性服務 toohello 無狀態模型建立和部署的 hello Machine Learning Studio 提供的介面。</span><span class="sxs-lookup"><span data-stu-id="a6c50-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="a6c50-117">批次執行服務 (BES) – 這是一種非同步的服務，為一批資料記錄進行計分。</span><span class="sxs-lookup"><span data-stu-id="a6c50-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="a6c50-118">如需 Machine Learning Web 服務的詳細資訊，請參閱[部署 Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="a6c50-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="a6c50-119">取得 Azure Machine Learning 授權金鑰</span><span class="sxs-lookup"><span data-stu-id="a6c50-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="a6c50-120">當您部署您的經驗時，會產生 API 金鑰 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="a6c50-121">您可以從數個位置擷取 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a6c50-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="a6c50-122">從 hello Microsoft Azure 機器學習 Web 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="a6c50-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="a6c50-123">登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net)入口網站。</span><span class="sxs-lookup"><span data-stu-id="a6c50-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="a6c50-124">新的機器學習 Web 服務的 tooretrieve hello API 金鑰：</span><span class="sxs-lookup"><span data-stu-id="a6c50-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="a6c50-125">在 hello Azure 機器學習 Web 服務入口網站中，按一下  **Web 服務**hello 上方的功能表。</span><span class="sxs-lookup"><span data-stu-id="a6c50-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="a6c50-126">按一下您想要的 tooretrieve hello 金鑰 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="a6c50-127">在 hello 上方功能表中，按一下 **取用**。</span><span class="sxs-lookup"><span data-stu-id="a6c50-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="a6c50-128">複製並儲存 hello**主索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="a6c50-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="a6c50-129">傳統的機器學習 Web 服務的 tooretrieve hello API 金鑰：</span><span class="sxs-lookup"><span data-stu-id="a6c50-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="a6c50-130">在 hello Azure 機器學習 Web 服務入口網站中，按一下 **傳統 Web 服務**hello 上方的功能表。</span><span class="sxs-lookup"><span data-stu-id="a6c50-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="a6c50-131">按一下您要使用的 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="a6c50-132">按一下您想要的 tooretrieve hello 金鑰 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="a6c50-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="a6c50-133">在 hello 上方功能表中，按一下 **取用**。</span><span class="sxs-lookup"><span data-stu-id="a6c50-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="a6c50-134">複製並儲存 hello**主索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="a6c50-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="a6c50-135">傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="a6c50-135">Classic Web service</span></span>
 <span data-ttu-id="a6c50-136">您也可以擷取從 Machine Learning Studio 或 hello Azure 傳統入口網站的傳統 Web 服務的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a6c50-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="a6c50-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="a6c50-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="a6c50-138">在機器學習 Studio 中，按一下  **WEB 服務**hello 左側。</span><span class="sxs-lookup"><span data-stu-id="a6c50-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="a6c50-139">按一下某個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-139">Click a Web service.</span></span> <span data-ttu-id="a6c50-140">hello **API 金鑰**位於 hello**儀表板** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a6c50-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="a6c50-141">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="a6c50-141">Azure classic portal</span></span>
1. <span data-ttu-id="a6c50-142">按一下**MACHINE LEARNING** hello 左側。</span><span class="sxs-lookup"><span data-stu-id="a6c50-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="a6c50-143">按一下您的 Web 服務所在的 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="a6c50-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="a6c50-144">按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="a6c50-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="a6c50-145">按一下某個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-145">Click a Web service.</span></span>
5. <span data-ttu-id="a6c50-146">按一下某個端點。</span><span class="sxs-lookup"><span data-stu-id="a6c50-146">Click an endpoint.</span></span> <span data-ttu-id="a6c50-147">hello 「 API 金鑰 」 已關閉在 hello 右下方。</span><span class="sxs-lookup"><span data-stu-id="a6c50-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="a6c50-148"><a id="connect"></a>Tooa 機器學習 Web 服務連接</span><span class="sxs-lookup"><span data-stu-id="a6c50-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="a6c50-149">您可以連接 tooa 使用任何支援 HTTP 要求和回應的程式設計語言的機器學習 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="a6c50-150">您可以從機器學習 Web 服務說明頁面檢視 C#、Python 和 R 的範例。</span><span class="sxs-lookup"><span data-stu-id="a6c50-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="a6c50-151">**機器學習服務 API 說明**當您部署 Web 服務時，會建立機器學習服務 API 說明。</span><span class="sxs-lookup"><span data-stu-id="a6c50-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="a6c50-152">請參閱 [Azure 機器學習逐步解說 - 部署 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="a6c50-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="a6c50-153">hello 機器學習 API 說明包含預測 Web 服務的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a6c50-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="a6c50-154">按一下您要使用的 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="a6c50-155">按一下您想要的 tooview hello API 說明頁面的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="a6c50-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="a6c50-156">在 hello 上方功能表中，按一下 **取用**。</span><span class="sxs-lookup"><span data-stu-id="a6c50-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="a6c50-157">按一下**API 說明頁面**hello 要求-回應] 或 [批次執行端點之下。</span><span class="sxs-lookup"><span data-stu-id="a6c50-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="a6c50-158">**tooview 機器學習 API 說明新的 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="a6c50-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="a6c50-159">在 hello Azure 機器學習 Web 服務入口網站：</span><span class="sxs-lookup"><span data-stu-id="a6c50-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="a6c50-160">按一下**WEB 服務**hello 上方功能表上。</span><span class="sxs-lookup"><span data-stu-id="a6c50-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="a6c50-161">按一下您想要的 tooretrieve hello 金鑰 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="a6c50-162">按一下**取用**tooget hello hello 要求 Reposonse 與 C#、 R 和 Python 中的批次執行服務和範例程式碼的 Uri。</span><span class="sxs-lookup"><span data-stu-id="a6c50-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="a6c50-163">按一下**Swagger API** tooget Swagger 根據文件 hello 應用程式開發介面呼叫 hello 從提供的 Uri。</span><span class="sxs-lookup"><span data-stu-id="a6c50-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="a6c50-164">C# 範例</span><span class="sxs-lookup"><span data-stu-id="a6c50-164">C# Sample</span></span>
<span data-ttu-id="a6c50-165">tooconnect tooa 機器學習 Web 服務，使用**HttpClient**傳遞 ScoreData。</span><span class="sxs-lookup"><span data-stu-id="a6c50-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="a6c50-166">ScoreData 包含 FeatureVector，代表 hello ScoreData n 維向量的數字的功能。</span><span class="sxs-lookup"><span data-stu-id="a6c50-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="a6c50-167">您 API 金鑰與驗證 toohello 機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="a6c50-168">tooconnect tooa 機器學習 Web 服務，hello **Microsoft.AspNet.WebApi.Client**必須安裝 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="a6c50-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="a6c50-169">**在 Visual Studio 中安裝 Microsoft.AspNet.WebApi.Client NuGet**</span><span class="sxs-lookup"><span data-stu-id="a6c50-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="a6c50-170">發行 hello 下載 UCI 資料集： 成人 2 類別的資料集 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="a6c50-171">按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="a6c50-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="a6c50-172">選擇 [ **Install-package Microsoft.AspNet.WebApi.Client**]。</span><span class="sxs-lookup"><span data-stu-id="a6c50-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="a6c50-173">**toorun hello 程式碼範例**</span><span class="sxs-lookup"><span data-stu-id="a6c50-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="a6c50-174">發行 」 範例 1： 下載 UCI 資料集： 成人 2 類別的資料集 」 實驗、 hello 機器學習範例集合的一部分。</span><span class="sxs-lookup"><span data-stu-id="a6c50-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="a6c50-175">指派 apiKey 與 hello 索引鍵，從 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="a6c50-176">請參閱前述的 **取得 Azure Machine Learning 授權金鑰** 。</span><span class="sxs-lookup"><span data-stu-id="a6c50-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="a6c50-177">指派 serviceUri 以 hello 要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="a6c50-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="a6c50-178">Python 範例</span><span class="sxs-lookup"><span data-stu-id="a6c50-178">Python Sample</span></span>
<span data-ttu-id="a6c50-179">tooconnect tooa 機器學習 Web 服務，使用 hello **urllib2**傳遞 ScoreData 程式庫。</span><span class="sxs-lookup"><span data-stu-id="a6c50-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="a6c50-180">ScoreData 包含 FeatureVector，代表 hello ScoreData n 維向量的數字的功能。</span><span class="sxs-lookup"><span data-stu-id="a6c50-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="a6c50-181">您 API 金鑰與驗證 toohello 機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="a6c50-182">**toorun hello 程式碼範例**</span><span class="sxs-lookup"><span data-stu-id="a6c50-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="a6c50-183">部署 」 範例 1： 下載 UCI 資料集： 成人 2 類別的資料集 」 實驗、 hello 機器學習範例集合的一部分。</span><span class="sxs-lookup"><span data-stu-id="a6c50-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="a6c50-184">指派 apiKey 與 hello 索引鍵，從 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6c50-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="a6c50-185">請參閱 hello**取得 Azure Machine Learning 授權金鑰**hello 開頭附近的這篇文章的一節。</span><span class="sxs-lookup"><span data-stu-id="a6c50-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="a6c50-186">指派 serviceUri 以 hello 要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="a6c50-186">Assign serviceUri with hello Request URI.</span></span>

