---
title: "從您的 Azure IoT 中樞 – Web 應用程式的感應器資料 aaaReal 時間資料視覺效果 |Microsoft 文件"
description: "使用 Microsoft Azure App Service toovisualize 氣溫和溼度資料會從 hello 感應器收集並傳送 tooyour Iot 中樞 hello Web 應用程式功能。"
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
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="33a1e-104">使用 hello Azure App Service Web 應用程式功能時，視覺化您的 Azure IoT 中樞的即時感應器資料</span><span class="sxs-lookup"><span data-stu-id="33a1e-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="33a1e-106">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="33a1e-106">What you learn</span></span>

<span data-ttu-id="33a1e-107">在此教學課程中，您學會 toovisualize 即時感應器資料 IoT 中樞接收執行 web 應用程式裝載 web 應用程式上的方式。</span><span class="sxs-lookup"><span data-stu-id="33a1e-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="33a1e-108">如果您想在 IoT 中樞的 tootry toovisualize hello 資料使用 Power BI，請參閱[使用 Power BI toovisualize 即時感應器資料從 Azure IoT 中樞](iot-hub-live-data-visualization-in-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="33a1e-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="33a1e-109">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="33a1e-109">What you do</span></span>

- <span data-ttu-id="33a1e-110">在 [hello Azure 入口網站中建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33a1e-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="33a1e-111">新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="33a1e-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="33a1e-112">設定 hello web 應用程式 tooread 感應器資料從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="33a1e-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="33a1e-113">上傳 web 應用程式 toobe hello web 應用程式所裝載。</span><span class="sxs-lookup"><span data-stu-id="33a1e-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="33a1e-114">開啟 hello web 應用程式 toosee 即時氣溫和溼度資料從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="33a1e-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="33a1e-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="33a1e-115">What you need</span></span>

- <span data-ttu-id="33a1e-116">[將裝置設定](iot-hub-raspberry-pi-kit-node-get-started.md)，其中涵蓋了 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="33a1e-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="33a1e-117">作用中的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="33a1e-117">An active Azure subscription</span></span>
  - <span data-ttu-id="33a1e-118">您訂用帳戶之下的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="33a1e-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="33a1e-119">用戶端應用程式所傳送訊息 tooyour Iot 中樞</span><span class="sxs-lookup"><span data-stu-id="33a1e-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="33a1e-120">下載 Git</span><span class="sxs-lookup"><span data-stu-id="33a1e-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="33a1e-121">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="33a1e-121">Create a web app</span></span>

1. <span data-ttu-id="33a1e-122">在 [hello [Azure 入口網站](https://ms.portal.azure.com/)，按一下 [**新增** > **Web + 行動** > **Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="33a1e-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="33a1e-123">輸入唯一的作業名稱，確認 hello 訂用帳戶，指定資源群組和位置，選取**Pin toodashboard**，然後按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="33a1e-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="33a1e-124">我們建議您選取 hello 與資源群組的相同位置。</span><span class="sxs-lookup"><span data-stu-id="33a1e-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="33a1e-125">這樣可協助處理速度並減少 hello 的資料傳輸成本。</span><span class="sxs-lookup"><span data-stu-id="33a1e-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![建立 Web 應用程式](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="33a1e-127">設定從 IoT 中樞 hello web 應用程式 tooread 資料</span><span class="sxs-lookup"><span data-stu-id="33a1e-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="33a1e-128">開啟您剛才佈建的 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33a1e-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="33a1e-129">按一下**應用程式設定**，然後在**應用程式設定**，加入下列索引鍵/值組的 hello:</span><span class="sxs-lookup"><span data-stu-id="33a1e-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="33a1e-130">Key</span><span class="sxs-lookup"><span data-stu-id="33a1e-130">Key</span></span>                                   | <span data-ttu-id="33a1e-131">值</span><span class="sxs-lookup"><span data-stu-id="33a1e-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="33a1e-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="33a1e-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="33a1e-133">取自 iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="33a1e-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="33a1e-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="33a1e-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="33a1e-135">hello 您加入 tooyour IoT 中樞的 hello 取用者群組名稱</span><span class="sxs-lookup"><span data-stu-id="33a1e-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![加入具有索引鍵/值組的設定 tooyour web 應用程式](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="33a1e-137">按一下**應用程式設定**下**一般設定**，切換 hello **Web 通訊端**選項，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="33a1e-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![切換 hello Web 通訊端選項](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="33a1e-139">上傳 hello web 應用程式所裝載的 web 應用程式 toobe</span><span class="sxs-lookup"><span data-stu-id="33a1e-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="33a1e-140">在 GitHub 上，我們已啟用 Web 應用程式 (web application)，以顯示 IoT 中樞的即時感應器資料。</span><span class="sxs-lookup"><span data-stu-id="33a1e-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="33a1e-141">您只需要 toodo 是與 Git 儲存機制設定 hello web 應用程式 toowork，請下載 hello web 應用程式從 GitHub，並再將它上傳的 hello web 應用程式 toohost tooAzure。</span><span class="sxs-lookup"><span data-stu-id="33a1e-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="33a1e-142">在 [hello web 應用程式中，按一下 [**部署選項** > **選擇來源** > **本機 Git 儲存機制**，然後按一下 [**確定**.</span><span class="sxs-lookup"><span data-stu-id="33a1e-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![設定 web 應用程式部署 toouse hello 本機 Git 儲存機制](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="33a1e-144">按一下**部署認證**，在 Azure 中建立的使用者名稱和密碼 toouse tooconnect toohello Git 儲存機制，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="33a1e-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="33a1e-145">按一下**概觀**，並記下的 hello 值**Git 複製 url**。</span><span class="sxs-lookup"><span data-stu-id="33a1e-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![取得 hello Git 複製 URL 的 web 應用程式](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="33a1e-147">開啟本機電腦上的命令或終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="33a1e-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="33a1e-148">從 GitHub 下載 hello web 應用程式，並將它上傳的 hello web 應用程式 toohost tooAzure。</span><span class="sxs-lookup"><span data-stu-id="33a1e-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="33a1e-149">toodo，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="33a1e-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="33a1e-150">\<Git 複製 URL\>是 hello hello hello 上找到的 Git 儲存機制 URL**概觀**hello web 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="33a1e-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="33a1e-151">開啟 hello web 應用程式 toosee 即時氣溫和溼度資料從 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="33a1e-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="33a1e-152">在 [hello**概觀**頁面的 web 應用程式，按一下 [hello URL tooopen hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33a1e-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![取得 web 應用程式的 hello URL](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="33a1e-154">您應該看到 hello 即時溫度和溼度資料從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="33a1e-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![顯示即時溫度和溼度的 Web 應用程式 (web app) 頁面](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="33a1e-156">確定 hello 範例應用程式正在執行您的裝置上。</span><span class="sxs-lookup"><span data-stu-id="33a1e-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="33a1e-157">如果沒有，就會空白圖表，您可以參考下的 toohello 教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="33a1e-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33a1e-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33a1e-158">Next steps</span></span>
<span data-ttu-id="33a1e-159">您已成功從 IoT 中樞使用 web 應用程式 toovisualize 即時感應器資料。</span><span class="sxs-lookup"><span data-stu-id="33a1e-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="33a1e-160">從 Azure IoT 中樞的替代方式 toovisualize 資料，請參閱[使用 Power BI toovisualize 即時感應器資料，或從 IoT 中樞](iot-hub-live-data-visualization-in-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="33a1e-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
