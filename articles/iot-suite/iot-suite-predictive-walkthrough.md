---
title: "aaaPredictive 維護逐步解說 |Microsoft 文件"
description: "逐步解說中的 hello Azure IoT 預測性維護預先設定的解決方案。"
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
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a><span data-ttu-id="bd252-103">預先設定的預測性維護解決方案逐步解說</span><span class="sxs-lookup"><span data-stu-id="bd252-103">Predictive maintenance preconfigured solution walkthrough</span></span>

<span data-ttu-id="bd252-104">hello 預先設定的預測性維護方案是預測 hello 點失敗時可能 toooccur 商務案例的端對端解決方案。</span><span class="sxs-lookup"><span data-stu-id="bd252-104">hello predictive maintenance preconfigured solution is an end-to-end solution for a business scenario that predicts hello point at which a failure is likely toooccur.</span></span> <span data-ttu-id="bd252-105">您可以針對最佳化維護等活動，主動使用此預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="bd252-105">You can use this preconfigured solution proactively for activities such as optimizing maintenance.</span></span> <span data-ttu-id="bd252-106">hello 解決方案結合索引鍵的 Azure IoT 套件服務，例如 IoT 中樞，串流分析和[Azure Machine Learning] [ lnk-machine-learning]工作區。</span><span class="sxs-lookup"><span data-stu-id="bd252-106">hello solution combines key Azure IoT Suite services, such as IoT Hub, Stream analytics, and an [Azure Machine Learning][lnk-machine-learning] workspace.</span></span> <span data-ttu-id="bd252-107">此工作區包含公用的範例資料集，toopredict hello 剩餘的生命週期 (RUL) 飛機引擎為基礎的模型。</span><span class="sxs-lookup"><span data-stu-id="bd252-107">This workspace contains a model, based on a public sample data set, toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="bd252-108">hello 方案完整實作做為您 tooplan 起點 hello IoT 商務案例，並實作符合特定的業務需求的解決方案。</span><span class="sxs-lookup"><span data-stu-id="bd252-108">hello solution fully implements hello IoT business scenario as a starting point for you tooplan and implement a solution that meets your own specific business requirements.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="bd252-109">邏輯架構</span><span class="sxs-lookup"><span data-stu-id="bd252-109">Logical architecture</span></span>

<span data-ttu-id="bd252-110">下列圖表中的 hello 概述 hello 邏輯解決方案元件的預先設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd252-110">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![][img-architecture]

<span data-ttu-id="bd252-111">hello 藍色項目是在 hello hello 預先設定方案的部署所在的地區中佈建的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="bd252-111">hello blue items are Azure services provisioned in hello region where you deployed hello preconfigured solution.</span></span> <span data-ttu-id="bd252-112">hello 您可以在其中部署預先設定的 hello 方案的地區清單會顯示 hello[佈建頁面][lnk-azureiotsuite]。</span><span class="sxs-lookup"><span data-stu-id="bd252-112">hello list of regions where you can deploy hello preconfigured solution displays on hello [provisioning page][lnk-azureiotsuite].</span></span>

<span data-ttu-id="bd252-113">hello 綠色項目是模擬的裝置，表示飛機引擎。</span><span class="sxs-lookup"><span data-stu-id="bd252-113">hello green item is a simulated device that represents an aircraft engine.</span></span> <span data-ttu-id="bd252-114">您可以深入了解這些模擬的裝置 hello 下列區段中。</span><span class="sxs-lookup"><span data-stu-id="bd252-114">You can learn more about these simulated devices in hello following section.</span></span>

<span data-ttu-id="bd252-115">hello 灰色項目代表可實作元件*裝置管理*功能。</span><span class="sxs-lookup"><span data-stu-id="bd252-115">hello gray items represent components that implement *device management* capabilities.</span></span> <span data-ttu-id="bd252-116">hello hello 預先設定的預測性維護方案目前版本不會提供這些資源。</span><span class="sxs-lookup"><span data-stu-id="bd252-116">hello current release of hello predictive maintenance preconfigured solution does not provision these resources.</span></span> <span data-ttu-id="bd252-117">toolearn 有關裝置管理的詳細資訊，請參閱 toohello[遠端監視預先設定的解決方案][lnk-remote-monitoring]。</span><span class="sxs-lookup"><span data-stu-id="bd252-117">toolearn more about device management, refer toohello [remote monitoring pre-configured solution][lnk-remote-monitoring].</span></span>

## <a name="simulated-devices"></a><span data-ttu-id="bd252-118">模擬的裝置</span><span class="sxs-lookup"><span data-stu-id="bd252-118">Simulated devices</span></span>

<span data-ttu-id="bd252-119">在預先設定的 hello 解決方案中，模擬的裝置會表示飛機引擎。</span><span class="sxs-lookup"><span data-stu-id="bd252-119">In hello preconfigured solution, a simulated device represents an aircraft engine.</span></span> <span data-ttu-id="bd252-120">hello 方案會使用兩個引擎對應 tooa 單一飛機佈建。</span><span class="sxs-lookup"><span data-stu-id="bd252-120">hello solution is provisioned with two engines that map tooa single aircraft.</span></span> <span data-ttu-id="bd252-121">每個引擎會發出四種類型的遙測： 感應器 9、 感應器 11、 感應器 14 和 15 感應器提供 hello 機器學習模型 toocalculate hello RUL hello 引擎所需的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="bd252-121">Each engine emits four types of telemetry: Sensor 9, Sensor 11, Sensor 14, and Sensor 15 provide hello data necessary for hello Machine Learning model toocalculate hello RUL for hello engine.</span></span> <span data-ttu-id="bd252-122">每個模擬的裝置會傳送下列遙測訊息 tooIoT 中樞 hello:</span><span class="sxs-lookup"><span data-stu-id="bd252-122">Each simulated device sends hello following telemetry messages tooIoT Hub:</span></span>

<span data-ttu-id="bd252-123">*週期計數*。</span><span class="sxs-lookup"><span data-stu-id="bd252-123">*Cycle count*.</span></span> <span data-ttu-id="bd252-124">週期表示已完成持續期間介於 2 小時與 10 小時之間的飛行。</span><span class="sxs-lookup"><span data-stu-id="bd252-124">A cycle represents a completed flight with a duration between two and ten hours.</span></span> <span data-ttu-id="bd252-125">Hello 飛行期間擷取每隔半小時遙測資料。</span><span class="sxs-lookup"><span data-stu-id="bd252-125">During hello flight, telemetry data is captured every half hour.</span></span>

<span data-ttu-id="bd252-126">*遙測*。</span><span class="sxs-lookup"><span data-stu-id="bd252-126">*Telemetry*.</span></span> <span data-ttu-id="bd252-127">有四個代表引擎屬性的感應器。</span><span class="sxs-lookup"><span data-stu-id="bd252-127">There are four sensors that represent engine attributes.</span></span> <span data-ttu-id="bd252-128">hello 感應器以一般方式標示為感應器 9、 感應器 11、 感應器 14 和 15 感應器。</span><span class="sxs-lookup"><span data-stu-id="bd252-128">hello sensors are generically labeled Sensor 9, Sensor 11, Sensor 14, and Sensor 15.</span></span> <span data-ttu-id="bd252-129">這些四個感應器從 hello RUL 模型代表遙測足夠 tooobtain 有用的結果。</span><span class="sxs-lookup"><span data-stu-id="bd252-129">These four sensors represent telemetry sufficient tooobtain useful results from hello RUL model.</span></span> <span data-ttu-id="bd252-130">使用預先設定的 hello 方案中的 hello model 是從公用的資料集，其中包含實際的引擎感應器資料建立。</span><span class="sxs-lookup"><span data-stu-id="bd252-130">hello model used in hello preconfigured solution is created from a public data set that includes real engine sensor data.</span></span> <span data-ttu-id="bd252-131">如需有關如何從原始資料集 hello hello 模型的建立方式的詳細資訊，請參閱 hello [Cortana 智慧組件庫預測維護範本][lnk-cortana-analytics]。</span><span class="sxs-lookup"><span data-stu-id="bd252-131">For more information on how hello model was created from hello original data set, see hello [Cortana Intelligence Gallery Predictive Maintenance Template][lnk-cortana-analytics].</span></span>

<span data-ttu-id="bd252-132">hello 模擬裝置可以處理下列命令從 hello 方案中的 hello IoT 中樞傳送的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd252-132">hello simulated devices can handle hello following commands sent from hello IoT hub in hello solution:</span></span>

| <span data-ttu-id="bd252-133">命令</span><span class="sxs-lookup"><span data-stu-id="bd252-133">Command</span></span> | <span data-ttu-id="bd252-134">說明</span><span class="sxs-lookup"><span data-stu-id="bd252-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bd252-135">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="bd252-135">StartTelemetry</span></span> |<span data-ttu-id="bd252-136">控制項 hello hello 模擬的狀態。</span><span class="sxs-lookup"><span data-stu-id="bd252-136">Controls hello state of hello simulation.</span></span><br/><span data-ttu-id="bd252-137">啟動 hello 裝置傳送遙測</span><span class="sxs-lookup"><span data-stu-id="bd252-137">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="bd252-138">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="bd252-138">StopTelemetry</span></span> |<span data-ttu-id="bd252-139">控制項 hello hello 模擬的狀態。</span><span class="sxs-lookup"><span data-stu-id="bd252-139">Controls hello state of hello simulation.</span></span><br/><span data-ttu-id="bd252-140">停駐點 hello 裝置傳送遙測</span><span class="sxs-lookup"><span data-stu-id="bd252-140">Stops hello device sending telemetry</span></span> |

<span data-ttu-id="bd252-141">IoT 中樞會提供裝置命令通知。</span><span class="sxs-lookup"><span data-stu-id="bd252-141">IoT Hub provides device command acknowledgment.</span></span>

## <a name="azure-stream-analytics-job"></a><span data-ttu-id="bd252-142">Azure 串流分析作業</span><span class="sxs-lookup"><span data-stu-id="bd252-142">Azure Stream Analytics job</span></span>

<span data-ttu-id="bd252-143">**作業： 遙測**運作 hello 傳入裝置遙測資料流上使用兩個陳述式：</span><span class="sxs-lookup"><span data-stu-id="bd252-143">**Job: Telemetry** operates on hello incoming device telemetry stream using two statements:</span></span>

* <span data-ttu-id="bd252-144">hello 第一次從 hello 裝置會選取所有的遙測資料，並傳送這個資料 tooblob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="bd252-144">hello first selects all telemetry from hello devices and sends this data tooblob storage.</span></span> <span data-ttu-id="bd252-145">從這裡開始，它會視覺化在 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd252-145">From here, it is visualized in hello web app.</span></span>
* <span data-ttu-id="bd252-146">平均感應器值兩分鐘的滑動視窗之上，並且傳送嗨事件中樞 tooan 透過此資料，第二個會計算 hello**事件處理器**。</span><span class="sxs-lookup"><span data-stu-id="bd252-146">hello second computes average sensor values over a two-minute sliding window and sends this data through hello Event hub tooan **event processor**.</span></span>

## <a name="event-processor"></a><span data-ttu-id="bd252-147">事件處理器</span><span class="sxs-lookup"><span data-stu-id="bd252-147">Event processor</span></span>
<span data-ttu-id="bd252-148">hello**事件處理器主機**Azure Web 工作中執行。</span><span class="sxs-lookup"><span data-stu-id="bd252-148">hello **event processor host** runs in an Azure Web Job.</span></span> <span data-ttu-id="bd252-149">hello**事件處理器**hello 平均感應器值所需完成的循環。</span><span class="sxs-lookup"><span data-stu-id="bd252-149">hello **event processor** takes hello average sensor values for a completed cycle.</span></span> <span data-ttu-id="bd252-150">接著，將這些值 tooan 引擎，定型的模型 toocalculate hello RUL 公開 （expose) 的 API。</span><span class="sxs-lookup"><span data-stu-id="bd252-150">It then passes those values tooan API that exposes trained model toocalculate hello RUL for an engine.</span></span> <span data-ttu-id="bd252-151">hello API 公開 Machine Learning 工作區佈建為 hello 方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="bd252-151">hello API is exposed by a Machine Learning workspace that is provisioned as part of hello solution.</span></span>

## <a name="machine-learning"></a><span data-ttu-id="bd252-152">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="bd252-152">Machine Learning</span></span>
<span data-ttu-id="bd252-153">hello 機器學習服務元件會使用衍生自真實飛機引擎從收集的資料模型。</span><span class="sxs-lookup"><span data-stu-id="bd252-153">hello Machine Learning component uses a model derived from data collected from real aircraft engines.</span></span> <span data-ttu-id="bd252-154">您可以瀏覽 toohello Machine Learning 工作區，從上 hello hello 磚[azureiotsuite.com] [ lnk-azureiotsuite]頁面為您佈建的方案。</span><span class="sxs-lookup"><span data-stu-id="bd252-154">You can navigate toohello Machine Learning workspace from hello tile on hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="bd252-155">hello 磚時，使用 hello 方案是在 hello**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="bd252-155">hello tile is available when hello solution is in hello **Ready** state.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bd252-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd252-156">Next steps</span></span>
<span data-ttu-id="bd252-157">現在您已看過 hello 的 hello 預先設定的預測性維護方案的重要元件，您可能會想 toocustomize 它。</span><span class="sxs-lookup"><span data-stu-id="bd252-157">Now you've seen hello key components of hello predictive maintenance preconfigured solution, you may want toocustomize it.</span></span> <span data-ttu-id="bd252-158">請參閱[自訂預先設定的解決方案指引][lnk-customize]。</span><span class="sxs-lookup"><span data-stu-id="bd252-158">See [Guidance on customizing preconfigured solutions][lnk-customize].</span></span>

<span data-ttu-id="bd252-159">您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：</span><span class="sxs-lookup"><span data-stu-id="bd252-159">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="bd252-160">[IoT 套件的常見問題集][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="bd252-160">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="bd252-161">[從 hello 接地 IoT 安全性][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="bd252-161">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/