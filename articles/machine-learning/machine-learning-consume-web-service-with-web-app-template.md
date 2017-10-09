---
title: "aaaConsume 機器學習 web 服務的 web 應用程式範本 |Microsoft 文件"
description: "在 Azure Marketplace tooconsume 在預測 web 服務，Azure Machine Learning 中使用的 web 應用程式範本。"
keywords: "Web 服務、operationalization、REST API、機器學習服務"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="a2eb0-104">使用 Azure Machine Learning Web 服務與 Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="a2eb0-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="a2eb0-105">一次您已開發預測模型並將它部署為 Azure web 服務使用 Machine Learning Studio 中，或使用 R 或 Python 之類的工具，您可以存取 hello 實際運作的模型，使用 REST API。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="a2eb0-106">有數種方式 tooconsume hello REST API 及存取 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="a2eb0-107">例如，您可以撰寫應用程式，在 C# 中，R，或使用 hello Python 部署 hello web 服務時，為您產生的程式碼範例 (用於 hello[機器學習 Web 服務網站](https://services.azureml.net/quickstart)或 hello web 服務儀表板中Machine Learning Studio)。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="a2eb0-108">您可以使用 hello 範例 Microsoft Excel 活頁簿為您建立在 hello 或相同的時間。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="a2eb0-109">但 hello web 服務是透過 hello hello 中提供的 Web 應用程式範本的最快速且輕鬆的方式 tooaccess [Azure Web 應用程式 Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/)。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="a2eb0-110">hello Azure 機器學習 Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="a2eb0-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="a2eb0-111">hello hello Azure Marketplace 中提供的 web 應用程式範本可以建立自訂的 web 應用程式知道您的 web 服務輸入的資料和預期的結果。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="a2eb0-112">您只需要 toodo 是提供 hello web 應用程式存取 tooyour web 服務和資料，並 hello 範本沒有 hello rest。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="a2eb0-113">兩個範本可供使用：</span><span class="sxs-lookup"><span data-stu-id="a2eb0-113">Two templates are available:</span></span>

* [<span data-ttu-id="a2eb0-114">Azure ML 要求回應服務 Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="a2eb0-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="a2eb0-115">Azure ML 批次執行服務 Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="a2eb0-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="a2eb0-116">每個範本會建立範例 ASP.NET 應用程式，您的 web 服務，使用 hello API URI 和金鑰，並將其部署為網站 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="a2eb0-117">hello 要求-回應服務 (RR) 範本會建立 web 應用程式，可讓您 toosend 資料 toohello web 服務 tooget 單一結果的單一資料列。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="a2eb0-118">hello 批次執行服務 (BES) 範本會建立 web 應用程式，可讓您 toosend 多個資料列的資料 tooget 多個結果。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="a2eb0-119">任何程式碼是必要的 toouse 這些範本。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="a2eb0-120">您只需要提供 hello API 金鑰和 URI，並 hello 範本建置 hello 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="a2eb0-121">tooget hello API 金鑰和 web 服務的要求 URI:</span><span class="sxs-lookup"><span data-stu-id="a2eb0-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="a2eb0-122">在 hello[服務入口網站](https://services.azureml.net/quickstart)，新的 web 服務，按一下  **Web 服務**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="a2eb0-123">或者，按一下 [傳統 Web 服務] \(對於傳統 Web 服務)。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="a2eb0-124">按一下您想 tooaccess hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="a2eb0-125">傳統 web 服務中，按一下您想要 tooaccess hello 端點。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="a2eb0-126">按一下**取用**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="a2eb0-127">複製 hello**主要**或**次要金鑰**並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="a2eb0-128">如果您要建立要求-回應服務 (RR) 範本，將複製 hello**要求-回應**URI 並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="a2eb0-129">如果您要建立批次執行服務 (BES) 範本，將複製 hello**批次要求**URI 並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="a2eb0-130">如何 toouse hello 要求-回應服務 (RR) 範本</span><span class="sxs-lookup"><span data-stu-id="a2eb0-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="a2eb0-131">依照這些步驟 toouse hello RR web 應用程式範本，hello 下列圖表所示。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![處理序 toouse RR 網站範本][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="a2eb0-133">移 toohello [Azure 入口網站](https://portal.azure.com)，**登入**，按一下 **新增**、 搜尋和選取**Azure ML 要求-回應服務 Web 應用程式**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="a2eb0-134">為您的 Web 應用程式提供唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-134">Give your web app a unique name.</span></span> <span data-ttu-id="a2eb0-135">hello hello web 應用程式的 URL 是此名稱，後面接著`.azurewebsites.net.`，例如`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="a2eb0-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="a2eb0-136">選取 hello Azure 訂用帳戶和服務執行您的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="a2eb0-137">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-137">Click **Create**.</span></span>
     
     ![建立 Web 應用程式][image5]

4. <span data-ttu-id="a2eb0-139">當 Azure 完成部署 hello web 應用程式時，按一下 hello **URL**在 hello 在 Azure 中，web 應用程式設定 頁面，或在網頁瀏覽器中輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="a2eb0-140">例如， `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="a2eb0-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="a2eb0-141">當 hello web 應用程式第一次執行它會要求您提供 hello **API Post URL**和**API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="a2eb0-142">輸入您稍早儲存的 hello 值 (**要求 URI**和**API 金鑰**分別)。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="a2eb0-143">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-143">Click **Submit**.</span></span>
     
     ![輸入貼文 URI 和 API 金鑰][image6]

6. <span data-ttu-id="a2eb0-145">hello web 應用程式會顯示其**Web 應用程式組態**hello 目前的 web 服務設定 頁面。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="a2eb0-146">這裡您可以進行變更 toohello hello web 應用程式所使用的設定。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a2eb0-147">變更此處 hello 設定只會變更此 web 應用程式它們。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="a2eb0-148">它不會變更您的 web 服務的 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="a2eb0-149">例如，如果您變更 hello**描述**這裡不會變更顯示 hello web 服務儀表板 Machine Learning Studio 中的 hello 描述。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="a2eb0-150">當您完成時，按一下**儲存變更**，然後按一下**移 tooHome 頁面**。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="a2eb0-151">從 hello 首頁上，您可以輸入值 toosend tooyour web 服務。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="a2eb0-152">按一下**送出**當您完成時，並將傳回 hello 的結果。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="a2eb0-153">如果您想 tooreturn toohello**組態**頁面上，移 toohello `setting.aspx` hello web 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="a2eb0-154">例如：`http://carprediction.azurewebsites.net/setting.aspx.`會提示的 tooenter hello API 金鑰一次-您需要 tooaccess hello 頁面，以及更新 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="a2eb0-155">您可以停止、 重新啟動，或刪除 hello hello 像任何其他 web 應用程式的 Azure 入口網站中的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="a2eb0-156">只要執行您可以瀏覽 toohello 家用 web 位址，並輸入新值。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="a2eb0-157">如何 toouse hello 批次執行服務 (BES) 範本</span><span class="sxs-lookup"><span data-stu-id="a2eb0-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="a2eb0-158">您可以使用 hello BES hello 相同方式為 hello RR 範本，除非建立該 hello web 應用程式中的 web 應用程式範本可讓您 toosubmit 多個資料列和接收多個結果。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="a2eb0-159">批次執行 web 服務的 hello 輸入的值可能來自 Azure 儲存體或本機檔案。hello 結果會儲存在 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="a2eb0-160">因此，您將需要 Azure 儲存體容器 toohold hello hello web 應用程式，所傳回的結果，您可能需要 tooget 您輸入的資料準備。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![處理 toouse BES 網站範本][image2]

1. <span data-ttu-id="a2eb0-162">後續 hello 相同程序 toocreate hello BES 太 web 應用程式與 hello RR 範本時，除了 go[Azure ML 批次執行服務 Web 應用程式範本](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)tooopen hello BES Azure Marketplace 範本，然後按一下**建立 Web 應用程式**.</span><span class="sxs-lookup"><span data-stu-id="a2eb0-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="a2eb0-163">您想要儲存，hello 結果 toospecify hello web 應用程式首頁上輸入 hello 目的地容器的資訊。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="a2eb0-164">也指定 hello web 應用程式可以從何處取得 hello 輸入的值，在本機檔案或 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="a2eb0-165">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-165">Click **Submit**.</span></span>
   
    ![儲存體資訊][image7]

<span data-ttu-id="a2eb0-167">hello web 應用程式將會顯示作業狀態的頁面。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="a2eb0-168">Hello 作業完成時將提供您在 Azure blob 儲存體中的 hello 結果 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="a2eb0-169">您也可以下載 hello 結果 tooa 本機檔案的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="a2eb0-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="a2eb0-170">取得詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a2eb0-170">For more information</span></span>
<span data-ttu-id="a2eb0-171">深入了解 toolearn...</span><span class="sxs-lookup"><span data-stu-id="a2eb0-171">toolearn more about...</span></span>

* <span data-ttu-id="a2eb0-172">使用 Machine Learning Studio 建立機器學習服務實驗，請參閱 [在 Azure Machine Learning Studio 中建立您的第一個實驗](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="a2eb0-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="a2eb0-173">如何 toodeploy 機器學習實驗為 web 服務，請參閱[部署 Azure 機器學習 web 服務](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="a2eb0-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="a2eb0-174">其他方式 tooaccess web 服務之後，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="a2eb0-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
