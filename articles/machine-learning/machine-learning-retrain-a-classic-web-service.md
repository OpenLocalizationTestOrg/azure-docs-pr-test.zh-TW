---
title: "重新訓練傳統 Web 服務 | Microsoft Docs"
description: "了解如何在 Azure Machine Learning 中以程式設計方式重新定型模型，以及使用新定型的模型來更新 Web 服務。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="065f4-103">重新訓練傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="065f4-103">Retrain a Classic web service</span></span>
<span data-ttu-id="065f4-104">您部署的預測性 Web 服務是預設評分端點。</span><span class="sxs-lookup"><span data-stu-id="065f4-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="065f4-105">預設端點會與原始定型和計分實驗同步，因此無法取代預設端點的定型模型。</span><span class="sxs-lookup"><span data-stu-id="065f4-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="065f4-106">若要重新訓練 Web 服務，必須在 Web 服務新增新端點。</span><span class="sxs-lookup"><span data-stu-id="065f4-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="065f4-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="065f4-107">Prerequisites</span></span>
<span data-ttu-id="065f4-108">您必須已設定訓練實驗與預測性實驗，如[以程式設計方式重新訓練機器學習服務模型](machine-learning-retrain-models-programmatically.md)中所示。</span><span class="sxs-lookup"><span data-stu-id="065f4-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="065f4-109">預測性實驗必須部署為傳統 Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="065f4-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="065f4-110">如需關於部署 Web 服務的其他資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="065f4-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="065f4-111">新增端點</span><span class="sxs-lookup"><span data-stu-id="065f4-111">Add a new Endpoint</span></span>
<span data-ttu-id="065f4-112">您部署的預測性 Web 服務包含預設評分端點，它會與原始定型和評分實驗定型的模型保持同步。</span><span class="sxs-lookup"><span data-stu-id="065f4-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="065f4-113">若要將您的 Web 服務更新為新訓練的模型，您必須建立新的評分端點。</span><span class="sxs-lookup"><span data-stu-id="065f4-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="065f4-114">在能以定型模型更新的預測性 Web 服務上，建立新的評分端點︰</span><span class="sxs-lookup"><span data-stu-id="065f4-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="065f4-115">請確定您將端點新增至預測性 Web 服務，而不是定型 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="065f4-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="065f4-116">如果您正確部署定型和預測性 Web 服務，您應該會看到列出兩個不同的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="065f4-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="065f4-117">預測性 Web 服務應是以 "[predictive exp.]" 結尾。</span><span class="sxs-lookup"><span data-stu-id="065f4-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="065f4-118">有三種方式可在 Web 服務新增端點︰</span><span class="sxs-lookup"><span data-stu-id="065f4-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="065f4-119">以程式設計方式</span><span class="sxs-lookup"><span data-stu-id="065f4-119">Programmatically</span></span>
2. <span data-ttu-id="065f4-120">使用 Microsoft Azure Web 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="065f4-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="065f4-121">使用 Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="065f4-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="065f4-122">以程式設計方式新增端點</span><span class="sxs-lookup"><span data-stu-id="065f4-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="065f4-123">您可以使用此 [GitHub 儲存機制](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)提供的範例程式碼來新增評分端點。</span><span class="sxs-lookup"><span data-stu-id="065f4-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="065f4-124">使用 Microsoft Azure Web 服務入口網站新增端點</span><span class="sxs-lookup"><span data-stu-id="065f4-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="065f4-125">在 Machine Learning Studio 中，按一下左側的 [Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="065f4-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="065f4-126">在 Web 服務儀表板底部，按一下 [管理端點預覽]。</span><span class="sxs-lookup"><span data-stu-id="065f4-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="065f4-127">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-127">Click **Add**.</span></span>
4. <span data-ttu-id="065f4-128">輸入新端點的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="065f4-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="065f4-129">選取記錄層級，以及是否啟用範例資料。</span><span class="sxs-lookup"><span data-stu-id="065f4-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="065f4-130">如需有關記錄的詳細資訊，請參閱 [為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="065f4-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="065f4-131">使用 Azure 傳統入口網站新增端點</span><span class="sxs-lookup"><span data-stu-id="065f4-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="065f4-132">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="065f4-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="065f4-133">按一下左側功能表中的 [Machine Learning] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="065f4-134">在 [名稱] 下，按一下您的工作區，然後按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="065f4-135">在 [名稱] 下，按一下 [普查模型 [predictive exp.]] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="065f4-136">按一下頁面底部的 [新增端點] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="065f4-137">如需有關新增端點的詳細資訊，請參閱 [建立端點](machine-learning-create-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="065f4-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="065f4-138">更新新增端點的定型模型</span><span class="sxs-lookup"><span data-stu-id="065f4-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="065f4-139">若要完成重新定型程序，您必須更新新增端點的定型模型。</span><span class="sxs-lookup"><span data-stu-id="065f4-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="065f4-140">如果您是使用 Azure 傳統入口網站新增端點，可在入口網站中按一下新端點的名稱，然後按一下 **UpdateResource** 連結，以取得您更新端點模型時所需的 URL。</span><span class="sxs-lookup"><span data-stu-id="065f4-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="065f4-141">如果您是使用範例程式碼新增端點，這會包含說明 URL 的位置 (靠輸出中的 HelpLocationURL  值識別)。</span><span class="sxs-lookup"><span data-stu-id="065f4-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="065f4-142">擷取路徑 URL：</span><span class="sxs-lookup"><span data-stu-id="065f4-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="065f4-143">將 URL 複製並貼到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="065f4-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="065f4-144">按一下 [更新資源] 連結。</span><span class="sxs-lookup"><span data-stu-id="065f4-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="065f4-145">複製 PATCH 要求的 POST URL。</span><span class="sxs-lookup"><span data-stu-id="065f4-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="065f4-146">例如：</span><span class="sxs-lookup"><span data-stu-id="065f4-146">For example:</span></span>
   
     <span data-ttu-id="065f4-147">修補程式 URL：https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="065f4-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="065f4-148">您現在可以使用定型模型來更新您先前建立的評分端點。</span><span class="sxs-lookup"><span data-stu-id="065f4-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="065f4-149">下列範例程式碼示範如何使用 *BaseLocation*、*RelativeLocation*、*SasBlobToken* 和 PATCH URL 來更新端點。</span><span class="sxs-lookup"><span data-stu-id="065f4-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="065f4-150">在端點儀表板上可以看到呼叫的 *apiKey* 與 *endpointUrl*。</span><span class="sxs-lookup"><span data-stu-id="065f4-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="065f4-151">*Resources* 中 *Name* 參數的值，應該符合預測性實驗中已儲存之訓練模型的「資源名稱」。</span><span class="sxs-lookup"><span data-stu-id="065f4-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="065f4-152">取得資源名稱：</span><span class="sxs-lookup"><span data-stu-id="065f4-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="065f4-153">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="065f4-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="065f4-154">按一下左側功能表中的 [Machine Learning] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="065f4-155">在 [名稱] 下，按一下您的工作區，然後按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="065f4-156">在 [名稱] 下，按一下 [普查模型 [predictive exp.]] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="065f4-157">按一下您新增的端點。</span><span class="sxs-lookup"><span data-stu-id="065f4-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="065f4-158">在端點儀表板中，按一下 [更新資源] 。</span><span class="sxs-lookup"><span data-stu-id="065f4-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="065f4-159">在 Web 服務的 [更新資源 API 文件] 頁面，您可以在 [可更新的資源] 下找到 [資源名稱]。</span><span class="sxs-lookup"><span data-stu-id="065f4-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="065f4-160">如果在您完成端點更新之前 SAS 權杖已到期，您必須執行 GET 以作業識別碼取得新的權杖。</span><span class="sxs-lookup"><span data-stu-id="065f4-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="065f4-161">程式碼執行成功後，新的端點應該會在大約 30 秒後開始使用重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="065f4-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="065f4-162">摘要</span><span class="sxs-lookup"><span data-stu-id="065f4-162">Summary</span></span>
<span data-ttu-id="065f4-163">使用重新定型 API 可以更新預測性 Web 服務的定型模型，運用於如下案例︰</span><span class="sxs-lookup"><span data-stu-id="065f4-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="065f4-164">定期以新的資料重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="065f4-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="065f4-165">散發模型給客戶，目的是要讓他們使用自己的資料重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="065f4-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="065f4-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="065f4-166">Next steps</span></span>
[<span data-ttu-id="065f4-167">Azure Machine Learning 傳統 Web 服務的重新訓練進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="065f4-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

