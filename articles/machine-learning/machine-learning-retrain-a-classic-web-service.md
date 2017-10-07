---
title: "aaaRetrain 傳統 web 服務 |Microsoft 文件"
description: "了解 tooprogrammatically 訓練模型和更新 hello web 服務 toouse hello 新定型的模型在 Azure Machine Learning 中的結果。"
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
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="70da9-103">重新訓練傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="70da9-103">Retrain a Classic web service</span></span>
<span data-ttu-id="70da9-104">評分端點的 hello 預設 hello 預測您部署的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="70da9-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="70da9-105">預設端點會保留與 hello 的同步處理原始定型和計分實驗，並因此 hello hello 預設端點已定型的模型無法取代。</span><span class="sxs-lookup"><span data-stu-id="70da9-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="70da9-106">tooretrain hello web 服務，您必須加入新的端點 toohello web 服務。</span><span class="sxs-lookup"><span data-stu-id="70da9-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="70da9-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="70da9-107">Prerequisites</span></span>
<span data-ttu-id="70da9-108">您必須已設定訓練實驗與預測性實驗，如[以程式設計方式重新訓練機器學習服務模型](machine-learning-retrain-models-programmatically.md)中所示。</span><span class="sxs-lookup"><span data-stu-id="70da9-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="70da9-109">hello 預測實驗必須部署為傳統機器學習 web 服務。</span><span class="sxs-lookup"><span data-stu-id="70da9-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="70da9-110">如需關於部署 Web 服務的其他資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="70da9-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="70da9-111">新增端點</span><span class="sxs-lookup"><span data-stu-id="70da9-111">Add a new Endpoint</span></span>
<span data-ttu-id="70da9-112">hello 預測您部署的 Web 服務包含預設的計分會保留與 hello 原始定型和計分實驗定型的模型的同步處理的端點。</span><span class="sxs-lookup"><span data-stu-id="70da9-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="70da9-113">tooupdate 您 web 服務 toowith 新定型的模型，您必須建立新的計分端點。</span><span class="sxs-lookup"><span data-stu-id="70da9-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="70da9-114">toocreate 新計分端點，則在 hello 可以隨 hello 定型模型的預測 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="70da9-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="70da9-115">請確定您要加入 hello 端點 toohello 預測的 Web 服務，hello 訓練 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="70da9-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="70da9-116">如果您正確部署定型和預測性 Web 服務，您應該會看到列出兩個不同的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="70da9-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="70da9-117">hello 預測 Web 服務應該以"[預測 exp 表示。] 結束。</span><span class="sxs-lookup"><span data-stu-id="70da9-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="70da9-118">有三種方式，您可以在其中加入新的結束點 tooa web 服務：</span><span class="sxs-lookup"><span data-stu-id="70da9-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="70da9-119">以程式設計方式</span><span class="sxs-lookup"><span data-stu-id="70da9-119">Programmatically</span></span>
2. <span data-ttu-id="70da9-120">使用 hello Microsoft Azure Web 服務的入口網站</span><span class="sxs-lookup"><span data-stu-id="70da9-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="70da9-121">使用 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="70da9-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="70da9-122">以程式設計方式新增端點</span><span class="sxs-lookup"><span data-stu-id="70da9-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="70da9-123">您可以加入使用 hello 範例程式碼中提供的計分端點[github 儲存機制](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)。</span><span class="sxs-lookup"><span data-stu-id="70da9-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="70da9-124">使用 hello Microsoft Azure Web 服務入口網站 tooadd 端點</span><span class="sxs-lookup"><span data-stu-id="70da9-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="70da9-125">在機器學習 Studio 中，在 hello 左側瀏覽資料行中，按一下 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="70da9-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="70da9-126">在 hello hello web 服務儀表板底部，按一下 **管理端點預覽**。</span><span class="sxs-lookup"><span data-stu-id="70da9-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="70da9-127">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="70da9-127">Click **Add**.</span></span>
4. <span data-ttu-id="70da9-128">輸入的名稱和描述 hello 新端點。</span><span class="sxs-lookup"><span data-stu-id="70da9-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="70da9-129">選取 hello 記錄層級，以及是否啟用範例資料。</span><span class="sxs-lookup"><span data-stu-id="70da9-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="70da9-130">如需有關記錄的詳細資訊，請參閱 [為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="70da9-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="70da9-131">使用 Azure 傳統入口網站 tooadd 端點 hello</span><span class="sxs-lookup"><span data-stu-id="70da9-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="70da9-132">登入 toohello[傳統 Azure 入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="70da9-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="70da9-133">在 hello 左窗格中，按一下  **Machine Learning**。</span><span class="sxs-lookup"><span data-stu-id="70da9-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="70da9-134">在 名稱 下，按一下您的工作區，然後按一下Web 服務 。</span><span class="sxs-lookup"><span data-stu-id="70da9-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="70da9-135">在 [名稱] 下，按一下 [普查模型 [predictive exp.]] 。</span><span class="sxs-lookup"><span data-stu-id="70da9-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="70da9-136">在 hello hello 頁面底部，按一下**加入端點**。</span><span class="sxs-lookup"><span data-stu-id="70da9-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="70da9-137">如需有關新增端點的詳細資訊，請參閱 [建立端點](machine-learning-create-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="70da9-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="70da9-138">更新 hello 加入端點的定型的模型</span><span class="sxs-lookup"><span data-stu-id="70da9-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="70da9-139">toocomplete hello 訓練程序，您必須更新 hello hello 您加入的新端點的定型的模型。</span><span class="sxs-lookup"><span data-stu-id="70da9-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="70da9-140">如果您加入 hello 使用 hello 傳統 Azure 入口網站的新端點，您可以按一下 hello 入口網站中的 hello 新端點的名稱，然後 hello **UpdateResource**連結 tooget hello URL，您需要 tooupdate hello 端點的模型。</span><span class="sxs-lookup"><span data-stu-id="70da9-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="70da9-141">如果您加入 hello 端點使用 hello 範例程式碼，這包括由 hello hello 說明 URL 位置*HelpLocationURL* hello 輸出中的值。</span><span class="sxs-lookup"><span data-stu-id="70da9-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="70da9-142">tooretrieve hello 路徑 URL:</span><span class="sxs-lookup"><span data-stu-id="70da9-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="70da9-143">複製並貼入您的瀏覽器中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="70da9-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="70da9-144">按一下 hello 更新資源連結。</span><span class="sxs-lookup"><span data-stu-id="70da9-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="70da9-145">將複製 hello 後的 hello PATCH 要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="70da9-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="70da9-146">例如：</span><span class="sxs-lookup"><span data-stu-id="70da9-146">For example:</span></span>
   
     <span data-ttu-id="70da9-147">修補程式 URL：https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="70da9-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="70da9-148">您現在可以使用 hello 定型的模型 tooupdate hello 計分您先前建立的端點。</span><span class="sxs-lookup"><span data-stu-id="70da9-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="70da9-149">下列範例程式碼的 hello 為您示範如何 toouse hello *BaseLocation*， *RelativeLocation*， *SasBlobToken*，和修補程式的 URL tooupdate hello 端點。</span><span class="sxs-lookup"><span data-stu-id="70da9-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="70da9-150">hello *apiKey*和 hello*端點 Url* hello 呼叫可以取得從端點儀表板。</span><span class="sxs-lookup"><span data-stu-id="70da9-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="70da9-151">hello 值 hello*名稱*中的參數*資源*應該符合 hello hello 資源名稱儲存已定型的模型在 hello 預測實驗中。</span><span class="sxs-lookup"><span data-stu-id="70da9-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="70da9-152">tooget hello 資源名稱：</span><span class="sxs-lookup"><span data-stu-id="70da9-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="70da9-153">登入 toohello[傳統 Azure 入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="70da9-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="70da9-154">在 hello 左窗格中，按一下  **Machine Learning**。</span><span class="sxs-lookup"><span data-stu-id="70da9-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="70da9-155">在 名稱 下，按一下您的工作區，然後按一下Web 服務 。</span><span class="sxs-lookup"><span data-stu-id="70da9-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="70da9-156">在 [名稱] 下，按一下 [普查模型 [predictive exp.]] 。</span><span class="sxs-lookup"><span data-stu-id="70da9-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="70da9-157">按一下 hello 您加入新的端點。</span><span class="sxs-lookup"><span data-stu-id="70da9-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="70da9-158">在 hello 端點儀表板上按一下**更新資源**。</span><span class="sxs-lookup"><span data-stu-id="70da9-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="70da9-159">您可以在 hello hello web 服務的更新資源應用程式開發介面文件頁面上，找到 hello**資源名稱**下**可更新資源**。</span><span class="sxs-lookup"><span data-stu-id="70da9-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="70da9-160">如果您的 SAS 權杖到期之前更新 hello 端點完成，您必須執行 GET 與 hello Id> tooobtain 新的權杖。</span><span class="sxs-lookup"><span data-stu-id="70da9-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="70da9-161">Hello 程式碼已成功執行時，應該啟動 hello 新端點，在大約 30 秒內使用 hello 重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="70da9-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="70da9-162">摘要</span><span class="sxs-lookup"><span data-stu-id="70da9-162">Summary</span></span>
<span data-ttu-id="70da9-163">使用 hello 重新訓練應用程式開發介面，您可以更新 hello 定型的模型的預測的 Web 服務，例如啟用案例：</span><span class="sxs-lookup"><span data-stu-id="70da9-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="70da9-164">定期以新的資料重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="70da9-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="70da9-165">Hello 目標是讓它們重新訓練 hello 模型使用自己的資料模型 toocustomers 的散發。</span><span class="sxs-lookup"><span data-stu-id="70da9-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70da9-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70da9-166">Next steps</span></span>
[<span data-ttu-id="70da9-167">疑難排解在 Azure Machine Learning 傳統的 web 服務的定型 hello</span><span class="sxs-lookup"><span data-stu-id="70da9-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

