---
title: "使用 Machine Learning Web 服務與 Web 應用程式範本 | Microsoft Docs"
description: "使用 Azure Marketplace 中的 Web 應用程式範本以使用 Azure Machine Learning 中的預測 Web 服務。"
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
ms.openlocfilehash: 95aa1fa23d83ec0dcd00870179167e803bafbd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="7cbe8-104">使用 Azure Machine Learning Web 服務與 Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="7cbe8-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="7cbe8-105">一旦使用 Machine Learning Studio，或使用 R 或 Python 之類的工具開發預測模型並部署為 Azure Web 服務後，即可使用 REST API 存取實際運作模型。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span></span>

<span data-ttu-id="7cbe8-106">有數種方法可以使用 REST API 和存取 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-106">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="7cbe8-107">例如，您可以使用當您部署 Web 服務 (可以在 [Machine Learning Web 服務入口網站](https://services.azureml.net/quickstart)或 Machine Learning Studio 中的 Web 服務儀表板取得) 時為您產生的範例程式碼，以 C#、R 或 Python 撰寫應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="7cbe8-108">或者，您可以同時使用為您建立的範例 Microsoft Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="7cbe8-109">但是最簡單快速存取 Web 服務的方式是透過 [Azure Web 應用程式 Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/)中提供的 Web 應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-azure-machine-learning-web-app-templates"></a><span data-ttu-id="7cbe8-110">Azure Machine Learning Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="7cbe8-110">The Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="7cbe8-111">Azure Marketplace 中可用的 Web 應用程式範本可以建立自訂的 Web 應用程式，該應用程式知道您的 Web 服務的輸入資料和預期的結果。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="7cbe8-112">您所需要做的就是將您的 Web 服務和資料的存取權授與 Web 應用程式，範本會執行其餘部分。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="7cbe8-113">兩個範本可供使用：</span><span class="sxs-lookup"><span data-stu-id="7cbe8-113">Two templates are available:</span></span>

* [<span data-ttu-id="7cbe8-114">Azure ML 要求回應服務 Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="7cbe8-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="7cbe8-115">Azure ML 批次執行服務 Web 應用程式範本</span><span class="sxs-lookup"><span data-stu-id="7cbe8-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="7cbe8-116">每個範本會建立範例 ASP.NET 應用程式，使用您的 Web 服務的 API URI 和金鑰，並做為網站部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span></span> <span data-ttu-id="7cbe8-117">要求回應服務 (RRS) 範本會建立 Web 應用程式，可讓您將資料的單一資料列傳送至 Web 服務以取得單一結果。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="7cbe8-118">批次執行服務 (BES) 範本會建立 Web 應用程式，可讓您傳送資料的許多資料列以取得多個結果。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="7cbe8-119">不必撰寫程式碼就可以使用這些範本。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-119">No coding is required to use these templates.</span></span> <span data-ttu-id="7cbe8-120">您只需提供 API 金鑰和 URI，範本就會為您建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-120">You just supply the API Key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="7cbe8-121">取得 Web 服務的 API 金鑰和要求 URI：</span><span class="sxs-lookup"><span data-stu-id="7cbe8-121">To get the API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="7cbe8-122">在 [Web 服務入口網站](https://services.azureml.net/quickstart)中，按一下頂端的 [Web 服務] \(對於新的 Web 服務)。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span></span> <span data-ttu-id="7cbe8-123">或者，按一下 [傳統 Web 服務] \(對於傳統 Web 服務)。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="7cbe8-124">按一下您想要存取的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-124">Click the web service you want to access.</span></span>
3. <span data-ttu-id="7cbe8-125">針對傳統 Web 服務，按一下您想要存取的端點。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-125">For a Classic web service, click the endpoint you want to access.</span></span>
4. <span data-ttu-id="7cbe8-126">按一下頂端的 [取用]。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-126">Click **Consume** at the top.</span></span>
5. <span data-ttu-id="7cbe8-127">複製**主要金鑰**或**次要金鑰**並儲存它。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-127">Copy the **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="7cbe8-128">如果您正在建立要求-回應服務 (RRS) 範本，請複製 **Request-Response** URI 並儲存它。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="7cbe8-129">如果您正在建立批次執行服務 (BES) 範本，請複製**批次要求** URI 並儲存˙它。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-rrs-template"></a><span data-ttu-id="7cbe8-130">如何使用要求回應服務 (RRS) 範本</span><span class="sxs-lookup"><span data-stu-id="7cbe8-130">How to use the Request-Response Service (RRS) template</span></span>
<span data-ttu-id="7cbe8-131">請依照下列步驟使用 RRS Web 應用程式範本，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![使用 RRS Web 範本的程序][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="7cbe8-133">移至 [Azure 入口網站](https://portal.azure.com)的 [登入]，按一下 [新增]，搜尋並選取 [Azure ML 要求-回應服務 Web 應用程式]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="7cbe8-134">為您的 Web 應用程式提供唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-134">Give your web app a unique name.</span></span> <span data-ttu-id="7cbe8-135">Web 應用程式的 URL 將是此名稱後面加上 `.azurewebsites.net.`。例如，`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="7cbe8-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="7cbe8-136">選擇 Azure 訂用帳戶及您的 Web 服務在其下執行的服務。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-136">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="7cbe8-137">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-137">Click **Create**.</span></span>
     
     ![建立 Web 應用程式][image5]

4. <span data-ttu-id="7cbe8-139">當 Azure 完成部署 Web 應用程式時，請按一下 Azure 中 Web 應用程式設定頁面上的 [URL]  ，或在網頁瀏覽器中輸入 URL。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="7cbe8-140">例如， `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="7cbe8-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="7cbe8-141">當 Web 應用程式第一次執行時，它會要求您提供 **API 貼文 URL** 和 **API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="7cbe8-142">輸入您先前儲存的值 (分別為**要求 URI** 和 **API 金鑰**)。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="7cbe8-143">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-143">Click **Submit**.</span></span>
     
     ![輸入貼文 URI 和 API 金鑰][image6]

6. <span data-ttu-id="7cbe8-145">Web 應用程式以目前 Web 服務設定顯示其 [Web 應用程式組態]  頁面。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-145">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="7cbe8-146">您可以在這裡變更 Web 應用程式所使用的設定。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-146">Here you can make changes to the settings used by the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7cbe8-147">變更此處的設定只會變更此 Web 應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-147">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="7cbe8-148">不會變更您的 Web 服務的預設設定。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-148">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="7cbe8-149">例如，如果您變更這裡的 [描述]  ，則不會變更在 Machine Learning Studio 中 Web 服務儀表板上顯示的描述。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="7cbe8-150">當您完成時，按一下 [儲存變更]，然後按一下 [到首頁]。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span></span>

7. <span data-ttu-id="7cbe8-151">您可以從首頁輸入值，以傳送至您的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-151">From the home page you can enter values to send to your web service.</span></span> <span data-ttu-id="7cbe8-152">當您完成時按一下 [提交]，將傳回結果。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-152">Click **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="7cbe8-153">如果您想要返回 [組態] 頁面上，請移至 Web 應用程式的 `setting.aspx` 頁面。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span></span> <span data-ttu-id="7cbe8-154">例如：`http://carprediction.azurewebsites.net/setting.aspx.`。系統會提示您再次輸入 API 金鑰，您需要該金鑰以存取頁面和更新設定。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span></span>

<span data-ttu-id="7cbe8-155">您可以在 Azure 入口網站停止、重新啟動或刪除 Web 應用程式，就像任何其他 Web 應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="7cbe8-156">只要它正在執行中，您就可以瀏覽至首頁網址並輸入新值。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-156">As long as it is running you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-bes-template"></a><span data-ttu-id="7cbe8-157">如何使用批次執行服務 (BES) 範本</span><span class="sxs-lookup"><span data-stu-id="7cbe8-157">How to use the Batch Execution Service (BES) template</span></span>
<span data-ttu-id="7cbe8-158">您可以使用與 RRS 範本相同的方式使用 BES Web 應用程式範本，不同的是建立的 Web 應用程式可讓您提交資料的多個資料列和接收多個結果。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="7cbe8-159">批次執行 Web 服務的輸入值可能來自 Azure 儲存體或本機檔案；結果會儲存在 Azure 儲存體容器中。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span></span>
<span data-ttu-id="7cbe8-160">因此，您需要 Azure 儲存體容器以存放 Web 應用程式所傳回的結果，您也必須準備好您的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span></span>

![使用 BES Web 範本的程序][image2]

1. <span data-ttu-id="7cbe8-162">依照與 RRS 範本相同的程序來建立 BES Web 應用程式 (除了移至 [Azure ML 批次執行服務 Web 應用程式範本](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)開啟 Azure Marketplace 上的 BES 範本並按一下 [建立 Web 應用程式] 之外)。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="7cbe8-163">若要指定您想要儲存結果的位置，請在 Web 應用程式的首頁上輸入目的地容器資訊。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span></span> <span data-ttu-id="7cbe8-164">同時指定 Web 應用程式可以在哪裡取得輸入值，在本機檔案或 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="7cbe8-165">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-165">Click **Submit**.</span></span>
   
    ![儲存體資訊][image7]

<span data-ttu-id="7cbe8-167">Web 應用程式將會顯示具有工作狀態的頁面。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-167">The web app will display a page with job status.</span></span>
<span data-ttu-id="7cbe8-168">工作完成時，系統會提供您 Azure Blob 儲存體中結果的位置。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span></span> <span data-ttu-id="7cbe8-169">您也可以選擇將結果下載到本機檔案。</span><span class="sxs-lookup"><span data-stu-id="7cbe8-169">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="7cbe8-170">如需 Blob 的詳細資訊，</span><span class="sxs-lookup"><span data-stu-id="7cbe8-170">For more information</span></span>
<span data-ttu-id="7cbe8-171">深入了解...</span><span class="sxs-lookup"><span data-stu-id="7cbe8-171">To learn more about...</span></span>

* <span data-ttu-id="7cbe8-172">使用 Machine Learning Studio 建立機器學習服務實驗，請參閱 [在 Azure Machine Learning Studio 中建立您的第一個實驗](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="7cbe8-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="7cbe8-173">如何將您的機器學習服務實驗部署為 Web 服務，請參閱 [部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="7cbe8-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="7cbe8-174">關於存取 Web 服務的其他方式，請參閱[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="7cbe8-174">other ways to access your web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
