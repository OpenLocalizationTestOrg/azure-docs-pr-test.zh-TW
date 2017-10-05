---
title: "使用 Azure Machine Learning 搭配來自 IoT 中樞的資料進行氣象預報 | Microsoft Docs"
description: "使用 Azure Machine Learning，根據 IoT 中樞透過感應器收集的溫度和溼度資料來預測下雨的機會。"
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
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="aae0a-104">在 Azure Machine Learning 中使用 IoT 中樞的感應器資料進行氣象預報</span><span class="sxs-lookup"><span data-stu-id="aae0a-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="aae0a-106">機器學習服務是一項資料科學技術，協助電腦從現有的資料學習，以便預測未來的行為、結果和趨勢。</span><span class="sxs-lookup"><span data-stu-id="aae0a-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="aae0a-107">Azure Machine Learning 是雲端預測性分析服務，可讓您快速地建立預測模型，並將其部署為分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="aae0a-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="aae0a-108">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="aae0a-108">What you learn</span></span>

<span data-ttu-id="aae0a-109">了解如何使用 Azure Machine Learning 透過來自您的 Azure IoT 中樞的溫度和溼度資料執行氣象預報 (下雨的機會)。</span><span class="sxs-lookup"><span data-stu-id="aae0a-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="aae0a-110">下雨的機會是備妥的氣象預報模型的輸出。</span><span class="sxs-lookup"><span data-stu-id="aae0a-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="aae0a-111">此模型的建置是根據溫度和溼度的歷史資料來預測下雨的機會。</span><span class="sxs-lookup"><span data-stu-id="aae0a-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="aae0a-112">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="aae0a-112">What you do</span></span>

- <span data-ttu-id="aae0a-113">將氣象預報模型部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="aae0a-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="aae0a-114">新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="aae0a-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="aae0a-115">建立串流分析作業，以及設定作業：</span><span class="sxs-lookup"><span data-stu-id="aae0a-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="aae0a-116">從 IoT 中樞讀取溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="aae0a-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="aae0a-117">呼叫 Web 服務來取得降雨機會。</span><span class="sxs-lookup"><span data-stu-id="aae0a-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="aae0a-118">將結果儲存至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="aae0a-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="aae0a-119">使用 Microsoft Azure 儲存體總管來檢視氣象預報。</span><span class="sxs-lookup"><span data-stu-id="aae0a-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aae0a-120">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="aae0a-120">What you need</span></span>

- <span data-ttu-id="aae0a-121">完成涵蓋下列需求的[設定裝置](iot-hub-raspberry-pi-kit-node-get-started.md)教學課程︰</span><span class="sxs-lookup"><span data-stu-id="aae0a-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="aae0a-122">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="aae0a-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="aae0a-123">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="aae0a-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="aae0a-124">將訊息傳送到您 Azure IoT 中樞的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="aae0a-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="aae0a-125">Azure Machine Learning Studio 帳戶。</span><span class="sxs-lookup"><span data-stu-id="aae0a-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="aae0a-126">([免費試用 Machine Learning Studio](https://studio.azureml.net/))。</span><span class="sxs-lookup"><span data-stu-id="aae0a-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="aae0a-127">將氣象預報模型部署為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="aae0a-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="aae0a-128">移至 [氣象預報模型頁面](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1)。</span><span class="sxs-lookup"><span data-stu-id="aae0a-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="aae0a-129">在 Microsoft Azure Machine Leaning Studio 中按一下 [在 Studio 中開啟]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="aae0a-130">![在 Cortana Intelligence 資源庫中開啟氣象預報模型頁面](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="aae0a-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="aae0a-131">按一下 [執行] 來驗證模型中的步驟。</span><span class="sxs-lookup"><span data-stu-id="aae0a-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="aae0a-132">此步驟可能需要 2 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="aae0a-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="aae0a-133">![在 Azure Machine Learning Studio 中開啟氣象預報模型](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="aae0a-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="aae0a-134">按一下 [設定 Web 服務] > [預測性 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="aae0a-135">![在 Azure Machine Learning Studio 中部署氣象預報模型](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="aae0a-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="aae0a-136">在圖表中，將 [Web 服務輸入] 模組拖曳至接近 [評分模型] 模組附近的位置。</span><span class="sxs-lookup"><span data-stu-id="aae0a-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="aae0a-137">將 [Web 服務輸入] 模組連線至 [評分模型] 模組。</span><span class="sxs-lookup"><span data-stu-id="aae0a-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="aae0a-138">![在 Azure Machine Learning Studio 中連線兩個模組](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="aae0a-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="aae0a-139">按一下 [執行] 來驗證模型中的步驟。</span><span class="sxs-lookup"><span data-stu-id="aae0a-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="aae0a-140">按一下 [部署 Web 服務] 來將模型部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="aae0a-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="aae0a-141">在模型的儀表板上，下載**要求/回應**的 **Excel 2010 或舊版活頁簿**。</span><span class="sxs-lookup"><span data-stu-id="aae0a-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="aae0a-142">即使您電腦上執行較新版的 Excel，也務必下載**Excel 2010 或舊版活頁簿**。</span><span class="sxs-lookup"><span data-stu-id="aae0a-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![下載要求回應端點的 Excel](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="aae0a-144">開啟 Excel 活頁簿，請記下 **Web 服務 URL** 和**存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="aae0a-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="aae0a-145">設定、設定及執行串流分析作業</span><span class="sxs-lookup"><span data-stu-id="aae0a-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="aae0a-146">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="aae0a-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="aae0a-147">在 [Azure 入口網站](https://ms.portal.azure.com/)中，按一下 [新增] > [物聯網] > [串流分析作業]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="aae0a-148">輸入作業的以下資訊。</span><span class="sxs-lookup"><span data-stu-id="aae0a-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="aae0a-149">**作業名稱**：作業名稱。</span><span class="sxs-lookup"><span data-stu-id="aae0a-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="aae0a-150">此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="aae0a-150">The name must be globally unique.</span></span>

   <span data-ttu-id="aae0a-151">**資源群組**︰使用 IoT 中樞所用的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="aae0a-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="aae0a-152">**位置**︰使用與資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="aae0a-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="aae0a-153">**釘選至儀表板**︰核取此選項可讓您從儀表板輕鬆地存取 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="aae0a-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![在 Azure 中建立串流分析作業](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="aae0a-155">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="aae0a-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="aae0a-156">將輸入新增至串流分析作業</span><span class="sxs-lookup"><span data-stu-id="aae0a-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="aae0a-157">開啟串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="aae0a-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="aae0a-158">在 [作業拓撲] 之下，按一下 [輸入]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="aae0a-159">在 [輸入] 窗格中，按一下 [新增]，然後輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="aae0a-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="aae0a-160">**輸入別名**︰輸入的唯一別名。</span><span class="sxs-lookup"><span data-stu-id="aae0a-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="aae0a-161">**來源**︰選取 [IoT 中樞]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="aae0a-162">**取用者群組**：選取您建立的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="aae0a-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![在 Azure 中將輸入新增至串流分析作業](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="aae0a-164">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="aae0a-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="aae0a-165">將輸出新增至串流分析作業</span><span class="sxs-lookup"><span data-stu-id="aae0a-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="aae0a-166">在 [作業拓撲] 之下，按一下 [輸出]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="aae0a-167">在 [輸出] 窗格中，按一下 [新增]，然後輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="aae0a-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="aae0a-168">**輸出別名**︰輸出的唯一別名。</span><span class="sxs-lookup"><span data-stu-id="aae0a-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="aae0a-169">**接收器**：選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="aae0a-170">**儲存體帳戶**：您 Blob 儲存體的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="aae0a-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="aae0a-171">您可以建立儲存體帳戶，或使用現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="aae0a-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="aae0a-172">**容器**：儲存 Blob 所在位置的容器。</span><span class="sxs-lookup"><span data-stu-id="aae0a-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="aae0a-173">您可以建立容器或是使用現有的容器。</span><span class="sxs-lookup"><span data-stu-id="aae0a-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="aae0a-174">**事件序列化格式**：選取 [CSV]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-174">**Event serialization format**: Select **CSV**.</span></span>

   ![在 Azure 中將輸出新增至串流分析作業](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="aae0a-176">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="aae0a-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="aae0a-177">將功能新增至串流分析作業，以呼叫您所部署的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="aae0a-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="aae0a-178">在 [作業拓撲] 下，按一下 [函式] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="aae0a-179">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="aae0a-179">Enter the following information:</span></span>

   <span data-ttu-id="aae0a-180">**函式別名**：輸入 `machinelearning`。</span><span class="sxs-lookup"><span data-stu-id="aae0a-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="aae0a-181">**函式類型**：選取 [Azure ML]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="aae0a-182">**匯入選項**：選取 [從不同的訂用帳戶匯入]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="aae0a-183">**URL**：輸入您從 Excel 活頁簿記下的 Web 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="aae0a-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="aae0a-184">**金鑰**：輸入您從 Excel 活頁簿記下的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="aae0a-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![在 Azure 中將功能新增至串流分析作業](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="aae0a-186">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="aae0a-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="aae0a-187">設定串流分析作業的查詢</span><span class="sxs-lookup"><span data-stu-id="aae0a-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="aae0a-188">在 [作業拓撲] 之下，按一下 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="aae0a-189">將現有程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="aae0a-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="aae0a-190">使用作業的輸入別名取代 `[YourInputAlias]`。</span><span class="sxs-lookup"><span data-stu-id="aae0a-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="aae0a-191">使用作業的輸出別名取代 `[YourOutputAlias]`。</span><span class="sxs-lookup"><span data-stu-id="aae0a-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="aae0a-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="aae0a-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="aae0a-193">執行串流分析作業</span><span class="sxs-lookup"><span data-stu-id="aae0a-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="aae0a-194">在串流分析作業中，按一下 [啟動] > [立即] > [啟動]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="aae0a-195">成功啟動作業後，作業狀態會從 [已停止] 變更為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![執行串流分析作業](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="aae0a-197">使用 Microsoft Azure 儲存體總管來檢視氣象預報</span><span class="sxs-lookup"><span data-stu-id="aae0a-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="aae0a-198">執行用戶端應用程式來開始收集和傳送溫度和溼度資料至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="aae0a-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="aae0a-199">對於 IoT 中樞收到的每個訊息，串流分析作業會呼叫氣象預報 Web 服務，以產生下雨的機會。</span><span class="sxs-lookup"><span data-stu-id="aae0a-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="aae0a-200">接著會將結果儲存到您的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="aae0a-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="aae0a-201">Azure 儲存體總管是一個工具，可供您用來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="aae0a-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="aae0a-202">[下載並安裝 Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="aae0a-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="aae0a-203">開啟 [Azure 儲存體總管]。</span><span class="sxs-lookup"><span data-stu-id="aae0a-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="aae0a-204">登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="aae0a-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="aae0a-205">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="aae0a-205">Select your subscription.</span></span>
1. <span data-ttu-id="aae0a-206">按一下您的訂用帳戶 > [儲存體帳戶] > 您的儲存體帳戶 > [Blob 容器] > 您的容器。</span><span class="sxs-lookup"><span data-stu-id="aae0a-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="aae0a-207">開啟 .csv 檔案來查看結果。</span><span class="sxs-lookup"><span data-stu-id="aae0a-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="aae0a-208">最後一個資料行記錄下雨的機會。</span><span class="sxs-lookup"><span data-stu-id="aae0a-208">The last column records the chance of rain.</span></span>

   ![使用 Azure Machine Learning 取得氣象預報結果](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="aae0a-210">摘要</span><span class="sxs-lookup"><span data-stu-id="aae0a-210">Summary</span></span>

<span data-ttu-id="aae0a-211">您已成功使用 Azure Machine Learning 根據 IoT 中樞收到的溫度和溼度資料來產生下雨的機會。</span><span class="sxs-lookup"><span data-stu-id="aae0a-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]