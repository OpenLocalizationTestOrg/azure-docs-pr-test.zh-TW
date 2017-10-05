---
title: "預測性維護逐步解說 | Microsoft Docs"
description: "預先設定之 Azure IoT 預測性維護解決方案的逐步解說。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: a68a8fdc3976ade0d1036d5ed58c8b2eb6d32a5d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a><span data-ttu-id="2389d-103">預先設定的預測性維護解決方案逐步解說</span><span class="sxs-lookup"><span data-stu-id="2389d-103">Predictive maintenance preconfigured solution walkthrough</span></span>

<span data-ttu-id="2389d-104">預先設定的預測性維護解決方案是一個端對端解決方案，適用於預測可能發生失敗之時間點的商務案例。</span><span class="sxs-lookup"><span data-stu-id="2389d-104">The predictive maintenance preconfigured solution is an end-to-end solution for a business scenario that predicts the point at which a failure is likely to occur.</span></span> <span data-ttu-id="2389d-105">您可以針對最佳化維護等活動，主動使用此預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="2389d-105">You can use this preconfigured solution proactively for activities such as optimizing maintenance.</span></span> <span data-ttu-id="2389d-106">此解決方案結合了主要 Azure IoT 套件服務，例如 IoT 中樞、串流分析和 [Azure Machine Learning][lnk-machine-learning] 工作區。</span><span class="sxs-lookup"><span data-stu-id="2389d-106">The solution combines key Azure IoT Suite services, such as IoT Hub, Stream analytics, and an [Azure Machine Learning][lnk-machine-learning] workspace.</span></span> <span data-ttu-id="2389d-107">此工作區包含以公開範例資料集為基礎的模型，用來預測飛機引擎的剩餘使用年限 (RUL)。</span><span class="sxs-lookup"><span data-stu-id="2389d-107">This workspace contains a model, based on a public sample data set, to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="2389d-108">此解決方案完整提供 IoT 商務案例的實作作為起點，讓您規劃和實作能滿足特定商務需求的解決方案。</span><span class="sxs-lookup"><span data-stu-id="2389d-108">The solution fully implements the IoT business scenario as a starting point for you to plan and implement a solution that meets your own specific business requirements.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="2389d-109">邏輯架構</span><span class="sxs-lookup"><span data-stu-id="2389d-109">Logical architecture</span></span>

<span data-ttu-id="2389d-110">下圖概述預先設定解決方案的邏輯元件：</span><span class="sxs-lookup"><span data-stu-id="2389d-110">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![][img-architecture]

<span data-ttu-id="2389d-111">藍色項目是在您佈建預先設定之解決方案的區域中所佈建的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="2389d-111">The blue items are Azure services provisioned in the region where you deployed the preconfigured solution.</span></span> <span data-ttu-id="2389d-112">您可以在其中部署預先設定之解決方案的地區清單會顯示於[佈建頁面][lnk-azureiotsuite]。</span><span class="sxs-lookup"><span data-stu-id="2389d-112">The list of regions where you can deploy the preconfigured solution displays on the [provisioning page][lnk-azureiotsuite].</span></span>

<span data-ttu-id="2389d-113">綠色項目是表示飛機引擎的模擬裝置。</span><span class="sxs-lookup"><span data-stu-id="2389d-113">The green item is a simulated device that represents an aircraft engine.</span></span> <span data-ttu-id="2389d-114">您可以在下一節中進一步了解這些模擬裝置。</span><span class="sxs-lookup"><span data-stu-id="2389d-114">You can learn more about these simulated devices in the following section.</span></span>

<span data-ttu-id="2389d-115">灰色項目代表可實作「裝置管理」功能的元件。</span><span class="sxs-lookup"><span data-stu-id="2389d-115">The gray items represent components that implement *device management* capabilities.</span></span> <span data-ttu-id="2389d-116">目前預先設定的預測性維護解決方案版本不會佈建這些資源。</span><span class="sxs-lookup"><span data-stu-id="2389d-116">The current release of the predictive maintenance preconfigured solution does not provision these resources.</span></span> <span data-ttu-id="2389d-117">若要深入了解裝置管理，請參閱[遠端監視預先設定的解決方案][lnk-remote-monitoring]。</span><span class="sxs-lookup"><span data-stu-id="2389d-117">To learn more about device management, refer to the [remote monitoring pre-configured solution][lnk-remote-monitoring].</span></span>

## <a name="simulated-devices"></a><span data-ttu-id="2389d-118">模擬的裝置</span><span class="sxs-lookup"><span data-stu-id="2389d-118">Simulated devices</span></span>

<span data-ttu-id="2389d-119">在預先設定的解決方案中，模擬裝置代表飛機引擎。</span><span class="sxs-lookup"><span data-stu-id="2389d-119">In the preconfigured solution, a simulated device represents an aircraft engine.</span></span> <span data-ttu-id="2389d-120">此解決方案已佈建兩個對應至單一飛機的引擎。</span><span class="sxs-lookup"><span data-stu-id="2389d-120">The solution is provisioned with two engines that map to a single aircraft.</span></span> <span data-ttu-id="2389d-121">每個引擎會發出四種類型的遙測：感應器 9、感應器 11、感應器 14 和感應器 15 會提供 Machine Learning 模型來計算該引擎的 RUL 所需的資料。</span><span class="sxs-lookup"><span data-stu-id="2389d-121">Each engine emits four types of telemetry: Sensor 9, Sensor 11, Sensor 14, and Sensor 15 provide the data necessary for the Machine Learning model to calculate the RUL for the engine.</span></span> <span data-ttu-id="2389d-122">每個模擬的裝置會將下列遙測訊息傳送至 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="2389d-122">Each simulated device sends the following telemetry messages to IoT Hub:</span></span>

<span data-ttu-id="2389d-123">*週期計數*。</span><span class="sxs-lookup"><span data-stu-id="2389d-123">*Cycle count*.</span></span> <span data-ttu-id="2389d-124">週期表示已完成持續期間介於 2 小時與 10 小時之間的飛行。</span><span class="sxs-lookup"><span data-stu-id="2389d-124">A cycle represents a completed flight with a duration between two and ten hours.</span></span> <span data-ttu-id="2389d-125">在飛行期間，每半小時擷取一次遙測資料。</span><span class="sxs-lookup"><span data-stu-id="2389d-125">During the flight, telemetry data is captured every half hour.</span></span>

<span data-ttu-id="2389d-126">*遙測*。</span><span class="sxs-lookup"><span data-stu-id="2389d-126">*Telemetry*.</span></span> <span data-ttu-id="2389d-127">有四個代表引擎屬性的感應器。</span><span class="sxs-lookup"><span data-stu-id="2389d-127">There are four sensors that represent engine attributes.</span></span> <span data-ttu-id="2389d-128">這些感應器會一般會標示為感應器 9、感應器 11、感應器 14 和感應器 15。</span><span class="sxs-lookup"><span data-stu-id="2389d-128">The sensors are generically labeled Sensor 9, Sensor 11, Sensor 14, and Sensor 15.</span></span> <span data-ttu-id="2389d-129">這 4 個感應器代表足以從 RUL 模型取得有用結果的遙測。</span><span class="sxs-lookup"><span data-stu-id="2389d-129">These four sensors represent telemetry sufficient to obtain useful results from the RUL model.</span></span> <span data-ttu-id="2389d-130">用於預先設定之解決方案中的模型是根據包含實際引擎感應器資料的公用資料集建立而來。</span><span class="sxs-lookup"><span data-stu-id="2389d-130">The model used in the preconfigured solution is created from a public data set that includes real engine sensor data.</span></span> <span data-ttu-id="2389d-131">如需有關如何從原始資料集建立模型的詳細資訊，請參閱 [Cortana Intelligence Gallery 預測性維護範本][lnk-cortana-analytics]。</span><span class="sxs-lookup"><span data-stu-id="2389d-131">For more information on how the model was created from the original data set, see the [Cortana Intelligence Gallery Predictive Maintenance Template][lnk-cortana-analytics].</span></span>

<span data-ttu-id="2389d-132">模擬的裝置可以處理從解決方案中 IoT 中樞傳送的下列命令：</span><span class="sxs-lookup"><span data-stu-id="2389d-132">The simulated devices can handle the following commands sent from the IoT hub in the solution:</span></span>

| <span data-ttu-id="2389d-133">命令</span><span class="sxs-lookup"><span data-stu-id="2389d-133">Command</span></span> | <span data-ttu-id="2389d-134">說明</span><span class="sxs-lookup"><span data-stu-id="2389d-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2389d-135">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="2389d-135">StartTelemetry</span></span> |<span data-ttu-id="2389d-136">控制模擬的狀態。</span><span class="sxs-lookup"><span data-stu-id="2389d-136">Controls the state of the simulation.</span></span><br/><span data-ttu-id="2389d-137">傳送遙測以啟動裝置</span><span class="sxs-lookup"><span data-stu-id="2389d-137">Starts the device sending telemetry</span></span> |
| <span data-ttu-id="2389d-138">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="2389d-138">StopTelemetry</span></span> |<span data-ttu-id="2389d-139">控制模擬的狀態。</span><span class="sxs-lookup"><span data-stu-id="2389d-139">Controls the state of the simulation.</span></span><br/><span data-ttu-id="2389d-140">傳送遙測以停止裝置</span><span class="sxs-lookup"><span data-stu-id="2389d-140">Stops the device sending telemetry</span></span> |

<span data-ttu-id="2389d-141">IoT 中樞會提供裝置命令通知。</span><span class="sxs-lookup"><span data-stu-id="2389d-141">IoT Hub provides device command acknowledgment.</span></span>

## <a name="azure-stream-analytics-job"></a><span data-ttu-id="2389d-142">Azure 串流分析作業</span><span class="sxs-lookup"><span data-stu-id="2389d-142">Azure Stream Analytics job</span></span>

<span data-ttu-id="2389d-143">**作業：遙測**會使用兩個陳述式來操作傳入裝置遙測串流：</span><span class="sxs-lookup"><span data-stu-id="2389d-143">**Job: Telemetry** operates on the incoming device telemetry stream using two statements:</span></span>

* <span data-ttu-id="2389d-144">第一個陳述式會從裝置選取所有遙測資料，然後將此資料傳送至 bob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2389d-144">The first selects all telemetry from the devices and sends this data to blob storage.</span></span> <span data-ttu-id="2389d-145">從這裡，它會呈現在 Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="2389d-145">From here, it is visualized in the web app.</span></span>
* <span data-ttu-id="2389d-146">第二個陳述式會透過兩分鐘的滑動視窗計算感應器平均值，然後透過事件中樞將此資料傳送至**事件處理器**。</span><span class="sxs-lookup"><span data-stu-id="2389d-146">The second computes average sensor values over a two-minute sliding window and sends this data through the Event hub to an **event processor**.</span></span>

## <a name="event-processor"></a><span data-ttu-id="2389d-147">事件處理器</span><span class="sxs-lookup"><span data-stu-id="2389d-147">Event processor</span></span>
<span data-ttu-id="2389d-148">**事件處理器主機**會在 Azure Web 作業中執行。</span><span class="sxs-lookup"><span data-stu-id="2389d-148">The **event processor host** runs in an Azure Web Job.</span></span> <span data-ttu-id="2389d-149">**事件處理器** 需要一個完整的週期來處理平均感應器值。</span><span class="sxs-lookup"><span data-stu-id="2389d-149">The **event processor** takes the average sensor values for a completed cycle.</span></span> <span data-ttu-id="2389d-150">接著將這些值傳遞至 API，該 API 會公開定型模型來計算引擎的 RUL。</span><span class="sxs-lookup"><span data-stu-id="2389d-150">It then passes those values to an API that exposes trained model to calculate the RUL for an engine.</span></span> <span data-ttu-id="2389d-151">此 API 是由佈建為方案一部分的 Machine Learning 工作區所公開。</span><span class="sxs-lookup"><span data-stu-id="2389d-151">The API is exposed by a Machine Learning workspace that is provisioned as part of the solution.</span></span>

## <a name="machine-learning"></a><span data-ttu-id="2389d-152">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="2389d-152">Machine Learning</span></span>
<span data-ttu-id="2389d-153">Machine Learning 元件使用的模型衍生自從真實飛機引擎收集而來的資料。</span><span class="sxs-lookup"><span data-stu-id="2389d-153">The Machine Learning component uses a model derived from data collected from real aircraft engines.</span></span> <span data-ttu-id="2389d-154">您可以從已佈建之解決方案的 [azureiotsuite.com][lnk-azureiotsuite] 頁面上的圖格，瀏覽至 Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="2389d-154">You can navigate to the Machine Learning workspace from the tile on the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="2389d-155">當解決方案處於**就緒**狀態時，就會出現此圖格。</span><span class="sxs-lookup"><span data-stu-id="2389d-155">The tile is available when the solution is in the **Ready** state.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2389d-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2389d-156">Next steps</span></span>
<span data-ttu-id="2389d-157">您現在已看到預先設定之預測性維護解決方案的主要元件，您可加以自訂。</span><span class="sxs-lookup"><span data-stu-id="2389d-157">Now you've seen the key components of the predictive maintenance preconfigured solution, you may want to customize it.</span></span> <span data-ttu-id="2389d-158">請參閱[自訂預先設定的解決方案指引][lnk-customize]。</span><span class="sxs-lookup"><span data-stu-id="2389d-158">See [Guidance on customizing preconfigured solutions][lnk-customize].</span></span>

<span data-ttu-id="2389d-159">您也可以瀏覽一些其他功能和預先設定的 IoT 套件解決方案的功能︰</span><span class="sxs-lookup"><span data-stu-id="2389d-159">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="2389d-160">[IoT 套件的常見問題集][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="2389d-160">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="2389d-161">[從頭建立 IoT 安全性][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="2389d-161">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/