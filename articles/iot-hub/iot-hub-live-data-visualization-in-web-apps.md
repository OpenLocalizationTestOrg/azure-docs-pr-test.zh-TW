---
title: "Azure IoT 中樞感應器資料的即時資料視覺效果 – Web Apps | Microsoft Docs"
description: "使用 Microsoft Azure App Service 的 Web Apps 功能來視覺化收集自感應器並傳送至 IoT 中樞的溫度和溼度資料。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "即時資料視覺效果, 即時資料視覺效果, 感應器資料視覺效果"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: e037f5c29cabf8e5d0d3e7ded187280a0652d5c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-the-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="c3f5b-104">使用 Azure App Service 的 Web Apps 功能將來自 Azure IoT 中樞的即時感應器資料視覺化</span><span class="sxs-lookup"><span data-stu-id="c3f5b-104">Visualize real-time sensor data from your Azure IoT hub by using the Web Apps feature of Azure App Service</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="c3f5b-106">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="c3f5b-106">What you learn</span></span>

<span data-ttu-id="c3f5b-107">在本教學課程中，您會了解如何執行 Web 應用程式 (web app) 上所裝載的 Web 應用程式 (web application)，將 IoT 中樞收到的即時感應器資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-107">In this tutorial, you learn how to visualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="c3f5b-108">如果您想嘗試使用 Power BI 將 IoT 中樞的資料視覺化，請參閱[使用 Power BI 將 Azure IoT 中樞的即時感應器資料視覺化](iot-hub-live-data-visualization-in-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-108">If you want to try to visualize the data in your IoT hub by using Power BI, see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c3f5b-109">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="c3f5b-109">What you do</span></span>

- <span data-ttu-id="c3f5b-110">在 Azure 入口網站中建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-110">Create a web app in the Azure portal.</span></span>
- <span data-ttu-id="c3f5b-111">新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="c3f5b-112">設定 Web 應用程式 (web app) 來讀取 IoT 中樞的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-112">Configure the web app to read sensor data from your IoT hub.</span></span>
- <span data-ttu-id="c3f5b-113">上傳要供 Web 應用程式 (web app) 裝載的 Web 應用程式 (web application)。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-113">Upload a web application to be hosted by the web app.</span></span>
- <span data-ttu-id="c3f5b-114">開啟 Web 應用程式 (web app)，以查看 IoT 中樞的即時溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c3f5b-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="c3f5b-115">What you need</span></span>

- <span data-ttu-id="c3f5b-116">[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)，其中涵蓋下列需求︰</span><span class="sxs-lookup"><span data-stu-id="c3f5b-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers the following requirements:</span></span>
  - <span data-ttu-id="c3f5b-117">作用中的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c3f5b-117">An active Azure subscription</span></span>
  - <span data-ttu-id="c3f5b-118">您訂用帳戶之下的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="c3f5b-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="c3f5b-119">將訊息傳送到 IoT 中樞的用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="c3f5b-119">A client application that sends messages to your Iot hub</span></span>
- [<span data-ttu-id="c3f5b-120">下載 Git</span><span class="sxs-lookup"><span data-stu-id="c3f5b-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="c3f5b-121">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c3f5b-121">Create a web app</span></span>

1. <span data-ttu-id="c3f5b-122">在 [Azure 入口網站](https://ms.portal.azure.com/)中，按一下 [新增] > [Web + 行動] >  [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-122">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="c3f5b-123">輸入唯一的作業名稱、驗證訂用帳戶、指定資源群組和位置，選取 [釘選到儀表板]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-123">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="c3f5b-124">我們建議您選取資源群組所在的相同位置。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-124">We recommend that you select the same location as that of your resource group.</span></span> <span data-ttu-id="c3f5b-125">這麼做有助於提升處理速度並減少資料傳輸成本。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-125">Doing so assists with processing speed and reduces the cost of data transfer.</span></span>

   ![建立 Web 應用程式](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-the-web-app-to-read-data-from-your-iot-hub"></a><span data-ttu-id="c3f5b-127">設定 Web 應用程式 (web app) 來讀取 IoT 中樞的資料</span><span class="sxs-lookup"><span data-stu-id="c3f5b-127">Configure the web app to read data from your IoT hub</span></span>

1. <span data-ttu-id="c3f5b-128">開啟您剛才佈建的 Web 應用程式 (web app)。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-128">Open the web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="c3f5b-129">按一下 [應用程式設定]，然後在 [應用程式設定] 之下，新增下列索引鍵/值組：</span><span class="sxs-lookup"><span data-stu-id="c3f5b-129">Click **Application settings**, and then, under **App settings**, add the following key/value pairs:</span></span>

   | <span data-ttu-id="c3f5b-130">金鑰</span><span class="sxs-lookup"><span data-stu-id="c3f5b-130">Key</span></span>                                   | <span data-ttu-id="c3f5b-131">值</span><span class="sxs-lookup"><span data-stu-id="c3f5b-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="c3f5b-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="c3f5b-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="c3f5b-133">取自 iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="c3f5b-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="c3f5b-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="c3f5b-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="c3f5b-135">您新增至 IoT 中樞之取用者群組的名稱</span><span class="sxs-lookup"><span data-stu-id="c3f5b-135">The name of the consumer group that you add to your IoT hub</span></span>  |

   ![使用索引鍵/值組將設定新增至 Web 應用程式 (web app)](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="c3f5b-137">按一下 [應用程式設定]，在 [一般設定] 之下切換 [Web 通訊端] 選項，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-137">Click **Application settings**, under **General settings**, toggle the **Web sockets** option, and then click **Save**.</span></span>

   ![切換 Web 通訊端選項](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-to-be-hosted-by-the-web-app"></a><span data-ttu-id="c3f5b-139">上傳要供 Web 應用程式 (web app) 裝載的 Web 應用程式 (web application)</span><span class="sxs-lookup"><span data-stu-id="c3f5b-139">Upload a web application to be hosted by the web app</span></span>

<span data-ttu-id="c3f5b-140">在 GitHub 上，我們已啟用 Web 應用程式 (web application)，以顯示 IoT 中樞的即時感應器資料。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="c3f5b-141">您只需要設定 Web 應用程式 (web app) 來使用 Git 存放庫、從 GitHub 下載 Web 應用程式 (web application)，然後將它上傳至 Azure 以供 Web 應用程式 (web app) 裝載。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-141">All you need to do is configure the web app to work with a Git repository, download the web application from GitHub, and then upload it to Azure for the web app to host.</span></span>

1. <span data-ttu-id="c3f5b-142">在 Web 應用程式 (web app) 中，按一下 [部署選項] > [選擇來源] > [本機 Git 存放庫]，然後 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-142">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![設定 Web 應用程式 (web app) 部署以使用本機 Git 存放庫](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="c3f5b-144">按一下 [部署認證]，建立要用來連線到 Azure 中 Git 存放庫的使用者名稱和密碼，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-144">Click **Deployment Credentials**, create a user name and password to use to connect to the Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="c3f5b-145">按一下 [概觀]，並記下 [Git 複製 url] 的值。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-145">Click **Overview**, and note the value of **Git clone url**.</span></span>

   ![取得 Web 應用程式 (web app) 的 Git 複製 URL](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="c3f5b-147">開啟本機電腦上的命令或終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="c3f5b-148">從 GitHub 下載 Web 應用程式 (web app)，然後將它上傳到 Azure 以供 Web 應用程式 (web app) 裝載。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-148">Download the web app from GitHub, and upload it to Azure for the web app to host.</span></span> <span data-ttu-id="c3f5b-149">若要這樣做，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="c3f5b-149">To do so, run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="c3f5b-150">\<Git clone URL\> 是在 Web 應用程式 (web app) 的 [概觀] 頁面上找到的 Git 儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-150">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span></span>

## <a name="open-the-web-app-to-see-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="c3f5b-151">開啟 Web 應用程式 (web app)，以查看 IoT 中樞的即時溫度和溼度資料</span><span class="sxs-lookup"><span data-stu-id="c3f5b-151">Open the web app to see real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="c3f5b-152">在 Web 應用程式 (web app) 的 [概觀] 頁面上，按一下 URL 以開啟 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-152">On the **Overview** page of your web app, click the URL to open the web app.</span></span>

![取得 Web 應用程式的 URL](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="c3f5b-154">您應該會看到 IoT 中樞的即時溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-154">You should see the real-time temperature and humidity data from your IoT hub.</span></span>

![顯示即時溫度和溼度的 Web 應用程式 (web app) 頁面](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="c3f5b-156">確保範例應用程式正在您的裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-156">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="c3f5b-157">若範例應用程式沒有在執行，您會看到空白的圖表，您可以參考[設定裝置](iot-hub-raspberry-pi-kit-node-get-started.md)下的教學。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-157">If not, you will get a blank chart, you can refer to the tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3f5b-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3f5b-158">Next steps</span></span>
<span data-ttu-id="c3f5b-159">您已成功使用 Web 應用程式 (web app) 將 IoT 中樞的即時感應器資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-159">You've successfully used your web app to visualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="c3f5b-160">如需將 IoT 中樞資料視覺化的其他方法，請參閱[使用 Power BI 將 Azure IoT 中樞的即時感應器資料視覺化](iot-hub-live-data-visualization-in-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="c3f5b-160">For an alternative way to visualize data from Azure IoT Hub, see [Use Power BI to visualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
