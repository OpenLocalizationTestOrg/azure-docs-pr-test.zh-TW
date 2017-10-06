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
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Azure Machine Learning 中使用 IoT 中樞的 hello 感應器資料的氣象預報預測

![端對端圖表](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

機器學習服務是一種技術可協助電腦從現有資料 tooforecast 未來行為、 結果，與趨勢的資料科學的其中一個。 Azure Machine Learning 會使得可能 tooquickly 雲端的預測分析服務建立及部署分析解決方案為預測模型。

## <a name="what-you-learn"></a>您學到什麼

您了解如何 toouse Azure Machine Learning toodo 氣象預報預測 （rain 機會） 使用 hello 氣溫和溼度的資料，從您的 Azure IoT 中樞。 hello 機會 rain 是 hello 輸出的已備妥的天氣預測模型。 hello 模型會根據 rain 根據氣溫和溼度的歷程資料 tooforecast 機率。

## <a name="what-you-do"></a>您要做什麼

- 部署為 web 服務的 hello 天氣預測模型。
- 新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。
- 建立串流分析工作，以及設定 hello 工作：
  - 從 IoT 中樞讀取溫度和溼度資料。
  - 呼叫 hello web 服務 tooget hello rain 的機率。
  - 儲存 hello 結果 tooan Azure blob 儲存體。
- 使用 Microsoft Azure 儲存體總管 tooview hello 氣象預報預測。

## <a name="what-you-need"></a>您需要什麼

- 教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：
  - 有效的 Azure 訂用帳戶。
  - 位於您訂用帳戶中的 Azure IoT 中樞。
  - 用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。
- Azure Machine Learning Studio 帳戶。 ([免費試用 Machine Learning Studio](https://studio.azureml.net/))。

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>部署為 web 服務的 hello 天氣預測模型

1. 移 toohello[天氣預測模型頁面](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1)。
1. 在 Microsoft Azure Machine Leaning Studio 中按一下 [在 Studio 中開啟]。
   ![Cortana 智慧組件庫中開啟 hello 天氣預測模型頁面](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. 按一下**執行**toovalidate hello hello 模型中的步驟。 此步驟可能會需要 toocomplete 2 分鐘。
   ![Azure Machine Learning Studio 中開啟 hello 天氣預測模型](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. 按一下 [設定 Web 服務] > [預測性 Web 服務]。
   ![部署 Azure Machine Learning Studio 中的 hello 天氣預測模型](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. 在 hello 圖表中，拖曳 hello **Web 服務輸入**某處附近 hello 模組**計分模型**模組。
1. 連接 hello **Web 服務輸入**模組 toohello**計分模型**模組。
   ![在 Azure Machine Learning Studio 中連線兩個模組](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. 按一下**執行**toovalidate hello hello 模型中的步驟。
1. 按一下**部署 WEB 服務**toodeploy hello 模型做為 web 服務。
1. 在儀表板 hello 的 hello 模型中，下載 hello **Excel 2010 或舊版的活頁簿**如**要求/回應**。

   > [!Note]
   > 請確定您下載 hello **Excel 2010 或舊版的活頁簿**即使您正在執行較新版的 Excel，您的電腦上。

   ![下載 hello Excel hello 要求的回應端點](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. 開啟 hello Excel 活頁簿，請記下 hello **WEB 服務 URL**和**便捷鍵**。

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>設定、設定及執行串流分析作業

### <a name="create-a-stream-analytics-job"></a>建立串流分析工作

1. 在 hello [Azure 入口網站](https://ms.portal.azure.com/)，按一下 **新增** > **物聯網** > **資料流分析工作**。
1. 輸入下列資訊為 hello 工作 hello。

   **工作名稱**: hello hello 作業名稱。 hello 名稱必須是全域唯一的。

   **資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。

   **位置**： 使用 hello 相同資源群組的位置。

   **Pin toodashboard**： 核取此選項，讓您輕鬆存取 tooyour IoT 中樞，從 hello 儀表板。

   ![在 Azure 中建立串流分析作業](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. 按一下 [建立] 。

### <a name="add-an-input-toohello-stream-analytics-job"></a>加入輸入的 toohello 資料流分析工作

1. 開啟 hello 資料流分析工作。
1. 在 [作業拓撲] 之下，按一下 [輸入]。
1. 在 [hello**輸入**] 窗格中，按一下**新增**，然後輸入下列資訊的 hello:

   **輸入的別名**: hello hello 輸入唯一別名。

   **來源**︰選取 [IoT 中樞]。

   **取用者群組**： 您建立選取 hello 取用者群組。

   ![在 Azure 中加入輸入的 toohello 資料流分析工作](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. 按一下 [建立] 。

### <a name="add-an-output-toohello-stream-analytics-job"></a>加入輸出 toohello 資料流分析工作

1. 在 [作業拓撲] 之下，按一下 [輸出]。
1. 在 [hello**輸出**] 窗格中，按一下**新增**，然後輸入下列資訊的 hello:

   **輸出別名**: hello hello 輸出的唯一別名。

   **接收器**：選取 [Blob 儲存體]。

   **儲存體帳戶**: hello 您的 blob 儲存體的儲存體帳戶。 您可以建立儲存體帳戶，或使用現有的帳戶。

   **容器**: hello 容器 hello blob 的儲存位置。 您可以建立容器或是使用現有的容器。

   **事件序列化格式**：選取 [CSV]。

   ![在 Azure 中加入輸出 toohello 資料流分析工作](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. 按一下 [建立] 。

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>新增函式 toohello Stream Analytics 工作 toocall hello web 服務部署

1. 在 [作業拓撲] 下，按一下 [函式] > [新增]。
1. 輸入下列資訊的 hello:

   **函式別名**：輸入 `machinelearning`。

   **函式類型**：選取 [Azure ML]。

   **匯入選項**：選取 [從不同的訂用帳戶匯入]。

   **URL**: hello 您記下下的 WEB 服務 URL 輸入 hello Excel 活頁簿。

   **索引鍵**: hello Excel 活頁簿輸入 hello 您記下下的便捷鍵。

   ![在 Azure 中加入函式 toohello 資料流分析工作](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. 按一下 [建立] 。

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>設定 hello hello 資料流分析作業的查詢

1. 在 [作業拓撲] 之下，按一下 [查詢]。
1. 取代下列程式碼的 hello hello 現有程式碼：

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   取代`[YourInputAlias]`hello 作業的 hello 輸入別名。

   取代`[YourOutputAlias]`hello 的 hello 工作的輸出別名。

1. 按一下 [儲存] 。

### <a name="run-hello-stream-analytics-job"></a>執行 hello 資料流分析工作

在 hello Stream Analytics 工作中，按一下 **啟動** > **現在** > **啟動**。 Hello 工作成功啟動 hello 作業狀態變更從**已停止**太**執行**。

![執行 hello 資料流分析工作](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>使用 Microsoft Azure 儲存體總管 tooview hello 氣象預報預測

執行 hello 用戶端應用程式 toostart 收集及傳送氣溫和溼度資料 tooyour IoT 中樞。 IoT 中樞接收每個訊息，hello 資料流分析工作會呼叫 hello 天氣預報網頁服務 tooproduce hello 的機會 rain。 然後儲存 hello 結果 tooyour Azure blob 儲存體。 Azure 儲存體總管是您可以使用 tooview hello 結果的工具。

1. [下載並安裝 Microsoft Azure 儲存體總管](http://storageexplorer.com/)。
1. 開啟 [Azure 儲存體總管]。
1. Azure 帳戶登入 tooyour。
1. 選取您的訂用帳戶。
1. 按一下您的訂用帳戶 > [儲存體帳戶] > 您的儲存體帳戶 > [Blob 容器] > 您的容器。
1. 開啟.csv 檔案 toosee hello 結果。 最後一個資料行記錄 hello hello rain 的機會。

   ![使用 Azure Machine Learning 取得氣象預報結果](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>摘要

您已成功地用 rain IoT 中樞收到 hello 氣溫和溼度資料為基礎的 Azure Machine Learning tooproduce hello 機會。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]