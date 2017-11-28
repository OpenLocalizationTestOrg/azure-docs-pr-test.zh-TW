---
title: "預測與從 IoT 中樞的資料搭配使用 Azure Machine Learning aaaWeather |Microsoft 文件"
description: "使用 Azure Machine Learning rain toopredict hello 機會根據 hello 氣溫和溼度 IoT 中心會收集從感應器的資料。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "氣象預報機器學習"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="66c8c-104">Azure Machine Learning 中使用 IoT 中樞的 hello 感應器資料的氣象預報預測</span><span class="sxs-lookup"><span data-stu-id="66c8c-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="66c8c-106">機器學習服務是一種技術可協助電腦從現有資料 tooforecast 未來行為、 結果，與趨勢的資料科學的其中一個。</span><span class="sxs-lookup"><span data-stu-id="66c8c-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="66c8c-107">Azure Machine Learning 會使得可能 tooquickly 雲端的預測分析服務建立及部署分析解決方案為預測模型。</span><span class="sxs-lookup"><span data-stu-id="66c8c-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="66c8c-108">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="66c8c-108">What you learn</span></span>

<span data-ttu-id="66c8c-109">您了解如何 toouse Azure Machine Learning toodo 氣象預報預測 （rain 機會） 使用 hello 氣溫和溼度的資料，從您的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="66c8c-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="66c8c-110">hello 機會 rain 是 hello 輸出的已備妥的天氣預測模型。</span><span class="sxs-lookup"><span data-stu-id="66c8c-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="66c8c-111">hello 模型會根據 rain 根據氣溫和溼度的歷程資料 tooforecast 機率。</span><span class="sxs-lookup"><span data-stu-id="66c8c-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="66c8c-112">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="66c8c-112">What you do</span></span>

- <span data-ttu-id="66c8c-113">部署為 web 服務的 hello 天氣預測模型。</span><span class="sxs-lookup"><span data-stu-id="66c8c-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="66c8c-114">新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="66c8c-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="66c8c-115">建立串流分析工作，以及設定 hello 工作：</span><span class="sxs-lookup"><span data-stu-id="66c8c-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="66c8c-116">從 IoT 中樞讀取溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="66c8c-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="66c8c-117">呼叫 hello web 服務 tooget hello rain 的機率。</span><span class="sxs-lookup"><span data-stu-id="66c8c-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="66c8c-118">儲存 hello 結果 tooan Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="66c8c-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="66c8c-119">使用 Microsoft Azure 儲存體總管 tooview hello 氣象預報預測。</span><span class="sxs-lookup"><span data-stu-id="66c8c-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="66c8c-120">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="66c8c-120">What you need</span></span>

- <span data-ttu-id="66c8c-121">教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="66c8c-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="66c8c-122">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c8c-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="66c8c-123">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="66c8c-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="66c8c-124">用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="66c8c-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="66c8c-125">Azure Machine Learning Studio 帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c8c-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="66c8c-126">([免費試用 Machine Learning Studio](https://studio.azureml.net/))。</span><span class="sxs-lookup"><span data-stu-id="66c8c-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="66c8c-127">部署為 web 服務的 hello 天氣預測模型</span><span class="sxs-lookup"><span data-stu-id="66c8c-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="66c8c-128">移 toohello[天氣預測模型頁面](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1)。</span><span class="sxs-lookup"><span data-stu-id="66c8c-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="66c8c-129">在 Microsoft Azure Machine Leaning Studio 中按一下 [在 Studio 中開啟]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="66c8c-130">![Cortana 智慧組件庫中開啟 hello 天氣預測模型頁面](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="66c8c-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="66c8c-131">按一下**執行**toovalidate hello hello 模型中的步驟。</span><span class="sxs-lookup"><span data-stu-id="66c8c-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="66c8c-132">此步驟可能會需要 toocomplete 2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="66c8c-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="66c8c-133">![Azure Machine Learning Studio 中開啟 hello 天氣預測模型](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="66c8c-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="66c8c-134">按一下 [設定 Web 服務] > [預測性 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="66c8c-135">![部署 Azure Machine Learning Studio 中的 hello 天氣預測模型](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="66c8c-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="66c8c-136">在 hello 圖表中，拖曳 hello **Web 服務輸入**某處附近 hello 模組**計分模型**模組。</span><span class="sxs-lookup"><span data-stu-id="66c8c-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="66c8c-137">連接 hello **Web 服務輸入**模組 toohello**計分模型**模組。</span><span class="sxs-lookup"><span data-stu-id="66c8c-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="66c8c-138">![在 Azure Machine Learning Studio 中連線兩個模組](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="66c8c-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="66c8c-139">按一下**執行**toovalidate hello hello 模型中的步驟。</span><span class="sxs-lookup"><span data-stu-id="66c8c-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="66c8c-140">按一下**部署 WEB 服務**toodeploy hello 模型做為 web 服務。</span><span class="sxs-lookup"><span data-stu-id="66c8c-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="66c8c-141">在儀表板 hello 的 hello 模型中，下載 hello **Excel 2010 或舊版的活頁簿**如**要求/回應**。</span><span class="sxs-lookup"><span data-stu-id="66c8c-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="66c8c-142">請確定您下載 hello **Excel 2010 或舊版的活頁簿**即使您正在執行較新版的 Excel，您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="66c8c-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![下載 hello Excel hello 要求的回應端點](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="66c8c-144">開啟 hello Excel 活頁簿，請記下 hello **WEB 服務 URL**和**便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="66c8c-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="66c8c-145">設定、設定及執行串流分析作業</span><span class="sxs-lookup"><span data-stu-id="66c8c-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="66c8c-146">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="66c8c-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="66c8c-147">在 hello [Azure 入口網站](https://ms.portal.azure.com/)，按一下 **新增** > **物聯網** > **資料流分析工作**。</span><span class="sxs-lookup"><span data-stu-id="66c8c-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="66c8c-148">輸入下列資訊為 hello 工作 hello。</span><span class="sxs-lookup"><span data-stu-id="66c8c-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="66c8c-149">**工作名稱**: hello hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="66c8c-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="66c8c-150">hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="66c8c-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="66c8c-151">**資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="66c8c-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="66c8c-152">**位置**： 使用 hello 相同資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="66c8c-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="66c8c-153">**Pin toodashboard**： 核取此選項，讓您輕鬆存取 tooyour IoT 中樞，從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="66c8c-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![在 Azure 中建立串流分析作業](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="66c8c-155">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="66c8c-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="66c8c-156">加入輸入的 toohello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="66c8c-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="66c8c-157">開啟 hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="66c8c-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="66c8c-158">在 [作業拓撲] 之下，按一下 [輸入]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="66c8c-159">在 [hello**輸入**] 窗格中，按一下**新增**，然後輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="66c8c-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="66c8c-160">**輸入的別名**: hello hello 輸入唯一別名。</span><span class="sxs-lookup"><span data-stu-id="66c8c-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="66c8c-161">**來源**︰選取 [IoT 中樞]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="66c8c-162">**取用者群組**： 您建立選取 hello 取用者群組。</span><span class="sxs-lookup"><span data-stu-id="66c8c-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![在 Azure 中加入輸入的 toohello 資料流分析工作](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="66c8c-164">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="66c8c-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="66c8c-165">加入輸出 toohello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="66c8c-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="66c8c-166">在 [作業拓撲] 之下，按一下 [輸出]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="66c8c-167">在 [hello**輸出**] 窗格中，按一下**新增**，然後輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="66c8c-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="66c8c-168">**輸出別名**: hello hello 輸出的唯一別名。</span><span class="sxs-lookup"><span data-stu-id="66c8c-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="66c8c-169">**接收器**：選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="66c8c-170">**儲存體帳戶**: hello 您的 blob 儲存體的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c8c-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="66c8c-171">您可以建立儲存體帳戶，或使用現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c8c-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="66c8c-172">**容器**: hello 容器 hello blob 的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="66c8c-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="66c8c-173">您可以建立容器或是使用現有的容器。</span><span class="sxs-lookup"><span data-stu-id="66c8c-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="66c8c-174">**事件序列化格式**：選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-174">**Event serialization format**: Select **CSV**.</span></span>

   ![在 Azure 中加入輸出 toohello 資料流分析工作](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="66c8c-176">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="66c8c-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="66c8c-177">新增函式 toohello Stream Analytics 工作 toocall hello web 服務部署</span><span class="sxs-lookup"><span data-stu-id="66c8c-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="66c8c-178">在 [作業拓撲] 下，按一下 [函式] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="66c8c-179">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="66c8c-179">Enter hello following information:</span></span>

   <span data-ttu-id="66c8c-180">**函式別名**：輸入 `machinelearning`。</span><span class="sxs-lookup"><span data-stu-id="66c8c-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="66c8c-181">**函式類型**：選取 [Azure ML]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="66c8c-182">**匯入選項**：選取 [從不同的訂用帳戶匯入]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="66c8c-183">**URL**: hello 您記下下的 WEB 服務 URL 輸入 hello Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="66c8c-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="66c8c-184">**索引鍵**: hello Excel 活頁簿輸入 hello 您記下下的便捷鍵。</span><span class="sxs-lookup"><span data-stu-id="66c8c-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![在 Azure 中加入函式 toohello 資料流分析工作](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="66c8c-186">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="66c8c-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="66c8c-187">設定 hello hello 資料流分析作業的查詢</span><span class="sxs-lookup"><span data-stu-id="66c8c-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="66c8c-188">在 [作業拓撲] 之下，按一下 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="66c8c-189">取代下列程式碼的 hello hello 現有程式碼：</span><span class="sxs-lookup"><span data-stu-id="66c8c-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="66c8c-190">取代`[YourInputAlias]`hello 作業的 hello 輸入別名。</span><span class="sxs-lookup"><span data-stu-id="66c8c-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="66c8c-191">取代`[YourOutputAlias]`hello 的 hello 工作的輸出別名。</span><span class="sxs-lookup"><span data-stu-id="66c8c-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="66c8c-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="66c8c-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="66c8c-193">執行 hello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="66c8c-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="66c8c-194">在 hello Stream Analytics 工作中，按一下 **啟動** > **現在** > **啟動**。</span><span class="sxs-lookup"><span data-stu-id="66c8c-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="66c8c-195">Hello 工作成功啟動 hello 作業狀態變更從**已停止**太**執行**。</span><span class="sxs-lookup"><span data-stu-id="66c8c-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![執行 hello 資料流分析工作](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="66c8c-197">使用 Microsoft Azure 儲存體總管 tooview hello 氣象預報預測</span><span class="sxs-lookup"><span data-stu-id="66c8c-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="66c8c-198">執行 hello 用戶端應用程式 toostart 收集及傳送氣溫和溼度資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="66c8c-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="66c8c-199">IoT 中樞接收每個訊息，hello 資料流分析工作會呼叫 hello 天氣預報網頁服務 tooproduce hello 的機會 rain。</span><span class="sxs-lookup"><span data-stu-id="66c8c-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="66c8c-200">然後儲存 hello 結果 tooyour Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="66c8c-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="66c8c-201">Azure 儲存體總管是您可以使用 tooview hello 結果的工具。</span><span class="sxs-lookup"><span data-stu-id="66c8c-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="66c8c-202">[下載並安裝 Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="66c8c-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="66c8c-203">開啟 [Azure 儲存體總管]。</span><span class="sxs-lookup"><span data-stu-id="66c8c-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="66c8c-204">Azure 帳戶登入 tooyour。</span><span class="sxs-lookup"><span data-stu-id="66c8c-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="66c8c-205">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c8c-205">Select your subscription.</span></span>
1. <span data-ttu-id="66c8c-206">按一下您的訂用帳戶 > [儲存體帳戶] > 您的儲存體帳戶 > [Blob 容器] > 您的容器。</span><span class="sxs-lookup"><span data-stu-id="66c8c-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="66c8c-207">開啟.csv 檔案 toosee hello 結果。</span><span class="sxs-lookup"><span data-stu-id="66c8c-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="66c8c-208">最後一個資料行記錄 hello hello rain 的機會。</span><span class="sxs-lookup"><span data-stu-id="66c8c-208">hello last column records hello chance of rain.</span></span>

   ![使用 Azure Machine Learning 取得氣象預報結果](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="66c8c-210">摘要</span><span class="sxs-lookup"><span data-stu-id="66c8c-210">Summary</span></span>

<span data-ttu-id="66c8c-211">您已成功地用 rain IoT 中樞收到 hello 氣溫和溼度資料為基礎的 Azure Machine Learning tooproduce hello 機會。</span><span class="sxs-lookup"><span data-stu-id="66c8c-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]