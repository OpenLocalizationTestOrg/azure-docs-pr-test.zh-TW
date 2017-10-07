---
title: "逐步解說中預先設定的監視解決方案 aaaRemote |Microsoft 文件"
description: "Hello 預先設定的 Azure IoT 解決方案遠端監視和其結構描述。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="e63c7-103">遠端監視預先設定解決方案逐步解說</span><span class="sxs-lookup"><span data-stu-id="e63c7-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="e63c7-104">hello IoT 套件遠端監視[預先設定的解決方案][ lnk-preconfigured-solutions]的端對端實作監視多部電腦執行遠端位置中的方案。</span><span class="sxs-lookup"><span data-stu-id="e63c7-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="e63c7-105">hello 解決方案結合主要 Azure 服務 tooprovide hello 的商務案例的泛型實作。</span><span class="sxs-lookup"><span data-stu-id="e63c7-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="e63c7-106">您可以做為起點使用 hello 解決方案，為您自己的實作和[自訂][ lnk-customize]它 toomeet 特定的業務需求。</span><span class="sxs-lookup"><span data-stu-id="e63c7-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="e63c7-107">本文將引導您完成一些 hello hello 遠端監視解決方案 tooenable 的索引鍵項目您 toounderstand 它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="e63c7-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="e63c7-108">這項知識能協助您︰</span><span class="sxs-lookup"><span data-stu-id="e63c7-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="e63c7-109">疑難排解 hello 方案中的問題。</span><span class="sxs-lookup"><span data-stu-id="e63c7-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="e63c7-110">規劃如何 toocustomize toohello 方案 toomeet 您自己的特定需求。</span><span class="sxs-lookup"><span data-stu-id="e63c7-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="e63c7-111">設計使用 Azure 服務的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="e63c7-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="e63c7-112">邏輯架構</span><span class="sxs-lookup"><span data-stu-id="e63c7-112">Logical architecture</span></span>

<span data-ttu-id="e63c7-113">下列圖表中的 hello 概述 hello 邏輯解決方案元件的預先設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="e63c7-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![邏輯架構](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="e63c7-115">模擬的裝置</span><span class="sxs-lookup"><span data-stu-id="e63c7-115">Simulated devices</span></span>

<span data-ttu-id="e63c7-116">預先設定的 hello 方案中 hello 模擬的裝置會代表冷卻裝置 （例如建置冷氣或設備空氣處理單元中）。</span><span class="sxs-lookup"><span data-stu-id="e63c7-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="e63c7-117">當您部署預先設定的 hello 方案時，您也會自動佈建執行中的四個模擬的裝置[Azure WebJob][lnk-webjobs]。</span><span class="sxs-lookup"><span data-stu-id="e63c7-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="e63c7-118">hello 模擬裝置方便您 tooexplore hello 方案行為的 hello hello 需要 toodeploy 沒有任何實體裝置。</span><span class="sxs-lookup"><span data-stu-id="e63c7-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="e63c7-119">toodeploy 實際實體裝置，請參閱 hello[連接您的裝置 toohello 遠端監視預先設定的解決方案][ lnk-connect-rm]教學課程。</span><span class="sxs-lookup"><span data-stu-id="e63c7-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="e63c7-120">裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="e63c7-120">Device-to-cloud messages</span></span>

<span data-ttu-id="e63c7-121">每個模擬的裝置皆可傳送下列訊息類型 tooIoT 中樞 hello:</span><span class="sxs-lookup"><span data-stu-id="e63c7-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="e63c7-122">訊息</span><span class="sxs-lookup"><span data-stu-id="e63c7-122">Message</span></span> | <span data-ttu-id="e63c7-123">說明</span><span class="sxs-lookup"><span data-stu-id="e63c7-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e63c7-124">啟動</span><span class="sxs-lookup"><span data-stu-id="e63c7-124">Startup</span></span> |<span data-ttu-id="e63c7-125">Hello 裝置啟動時，它會傳送**裝置資訊**toohello 後端包含與其本身相關的資訊訊息。</span><span class="sxs-lookup"><span data-stu-id="e63c7-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="e63c7-126">此資料包含 hello 裝置識別碼和 hello 命令的清單，而且方法 hello 裝置支援。</span><span class="sxs-lookup"><span data-stu-id="e63c7-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="e63c7-127">目前狀態</span><span class="sxs-lookup"><span data-stu-id="e63c7-127">Presence</span></span> |<span data-ttu-id="e63c7-128">裝置會定期傳送**存在**訊息 tooreport 是否 hello 裝置可以有意義的感應器的 hello 存在。</span><span class="sxs-lookup"><span data-stu-id="e63c7-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="e63c7-129">遙測</span><span class="sxs-lookup"><span data-stu-id="e63c7-129">Telemetry</span></span> |<span data-ttu-id="e63c7-130">裝置會定期傳送**遙測**報告模擬的值，如 hello 氣溫和溼度從 hello 裝置收集到的訊息的模擬感應器。</span><span class="sxs-lookup"><span data-stu-id="e63c7-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="e63c7-131">hello 方案會儲存 hello hello 裝置 Cosmos DB 資料庫中，而不是在 hello 裝置兩個支援的命令清單。</span><span class="sxs-lookup"><span data-stu-id="e63c7-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="e63c7-132">屬性和裝置對應項</span><span class="sxs-lookup"><span data-stu-id="e63c7-132">Properties and device twins</span></span>

<span data-ttu-id="e63c7-133">hello 模擬的裝置傳送 hello 下列裝置屬性 toohello[兩個][ lnk-device-twins]在 hello IoT 中樞與*報告屬性*。</span><span class="sxs-lookup"><span data-stu-id="e63c7-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="e63c7-134">hello 裝置傳送報告屬性，在啟動和回應 tooa**變更裝置狀態**命令或方法。</span><span class="sxs-lookup"><span data-stu-id="e63c7-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="e63c7-135">屬性</span><span class="sxs-lookup"><span data-stu-id="e63c7-135">Property</span></span> | <span data-ttu-id="e63c7-136">目的</span><span class="sxs-lookup"><span data-stu-id="e63c7-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="e63c7-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="e63c7-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="e63c7-138">頻率 （秒） hello 裝置傳送遙測</span><span class="sxs-lookup"><span data-stu-id="e63c7-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="e63c7-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="e63c7-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="e63c7-140">指定模擬的 hello 溫度遙測 hello 平均值</span><span class="sxs-lookup"><span data-stu-id="e63c7-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="e63c7-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="e63c7-141">Device.DeviceID</span></span> |<span data-ttu-id="e63c7-142">提供或裝置 hello 方案中建立時指派的識別碼</span><span class="sxs-lookup"><span data-stu-id="e63c7-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="e63c7-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="e63c7-143">Device.DeviceState</span></span> | <span data-ttu-id="e63c7-144">Hello 裝置所報告的狀態</span><span class="sxs-lookup"><span data-stu-id="e63c7-144">State reported by hello device</span></span> |
| <span data-ttu-id="e63c7-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="e63c7-145">Device.CreatedTime</span></span> |<span data-ttu-id="e63c7-146">建立時間 hello 裝置 hello 方案中</span><span class="sxs-lookup"><span data-stu-id="e63c7-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="e63c7-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="e63c7-147">Device.StartupTime</span></span> |<span data-ttu-id="e63c7-148">啟動時間 hello 裝置</span><span class="sxs-lookup"><span data-stu-id="e63c7-148">Time hello device was started</span></span> |
| <span data-ttu-id="e63c7-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="e63c7-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="e63c7-150">hello 版本號碼的 hello 最後所需的屬性變更</span><span class="sxs-lookup"><span data-stu-id="e63c7-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="e63c7-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="e63c7-151">Device.Location.Latitude</span></span> |<span data-ttu-id="e63c7-152">緯度 hello 裝置位置</span><span class="sxs-lookup"><span data-stu-id="e63c7-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="e63c7-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="e63c7-153">Device.Location.Longitude</span></span> |<span data-ttu-id="e63c7-154">經度 hello 裝置位置</span><span class="sxs-lookup"><span data-stu-id="e63c7-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="e63c7-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="e63c7-155">System.Manufacturer</span></span> |<span data-ttu-id="e63c7-156">裝置製造商</span><span class="sxs-lookup"><span data-stu-id="e63c7-156">Device manufacturer</span></span> |
| <span data-ttu-id="e63c7-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="e63c7-157">System.ModelNumber</span></span> |<span data-ttu-id="e63c7-158">Hello 裝置的模型數目</span><span class="sxs-lookup"><span data-stu-id="e63c7-158">Model number of hello device</span></span> |
| <span data-ttu-id="e63c7-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="e63c7-159">System.SerialNumber</span></span> |<span data-ttu-id="e63c7-160">Hello 裝置的序號</span><span class="sxs-lookup"><span data-stu-id="e63c7-160">Serial number of hello device</span></span> |
| <span data-ttu-id="e63c7-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="e63c7-161">System.FirmwareVersion</span></span> |<span data-ttu-id="e63c7-162">目前在 hello 裝置上的韌體版本</span><span class="sxs-lookup"><span data-stu-id="e63c7-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="e63c7-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="e63c7-163">System.Platform</span></span> |<span data-ttu-id="e63c7-164">Hello 裝置的平台架構</span><span class="sxs-lookup"><span data-stu-id="e63c7-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="e63c7-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="e63c7-165">System.Processor</span></span> |<span data-ttu-id="e63c7-166">處理器執行中的 hello 裝置</span><span class="sxs-lookup"><span data-stu-id="e63c7-166">Processor running hello device</span></span> |
| <span data-ttu-id="e63c7-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="e63c7-167">System.InstalledRAM</span></span> |<span data-ttu-id="e63c7-168">Hello 裝置上安裝的 RAM 數量</span><span class="sxs-lookup"><span data-stu-id="e63c7-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="e63c7-169">hello 模擬器植入模擬裝置的範例值中的這些屬性。</span><span class="sxs-lookup"><span data-stu-id="e63c7-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="e63c7-170">每次 hello 模擬器初始化模擬的裝置、 裝置 hello 報告 hello 預先定義的中繼資料 tooIoT 中樞為報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="e63c7-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="e63c7-171">報告的屬性只能由 hello 裝置更新。</span><span class="sxs-lookup"><span data-stu-id="e63c7-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="e63c7-172">toochange 報告屬性，您想要的屬性中設定方案入口網站。</span><span class="sxs-lookup"><span data-stu-id="e63c7-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="e63c7-173">負責 hello hello 裝置：</span><span class="sxs-lookup"><span data-stu-id="e63c7-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="e63c7-174">定期擷取 hello IoT 中樞所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="e63c7-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="e63c7-175">包含所需的 hello 屬性值更新其設定。</span><span class="sxs-lookup"><span data-stu-id="e63c7-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="e63c7-176">以報告屬性，傳送 hello 新值後 toohello 中樞。</span><span class="sxs-lookup"><span data-stu-id="e63c7-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="e63c7-177">從 hello 方案儀表板，您可以使用*所需屬性*tooset 屬性上的裝置使用 hello[裝置兩個][lnk-device-twins]。</span><span class="sxs-lookup"><span data-stu-id="e63c7-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="e63c7-178">一般而言，裝置會從回時報告屬性，變更其內部狀態和報告 hello hello 中樞 tooupdate 讀取所需的屬性值。</span><span class="sxs-lookup"><span data-stu-id="e63c7-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="e63c7-179">hello 模擬的裝置的程式碼只會使用 hello **Desired.Config.TemperatureMeanValue**和**Desired.Config.TelemetryInterval**需的屬性 tooupdate hello 報告傳送回屬性tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="e63c7-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="e63c7-180">所有其他想要的屬性變更要求會遭到忽略 hello 模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="e63c7-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="e63c7-181">方法</span><span class="sxs-lookup"><span data-stu-id="e63c7-181">Methods</span></span>

<span data-ttu-id="e63c7-182">hello 模擬的裝置可以處理下列方法 hello ([直接方法][lnk-direct-methods]) 從 hello 方案入口網站來完成 hello IoT 中樞叫用：</span><span class="sxs-lookup"><span data-stu-id="e63c7-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="e63c7-183">方法</span><span class="sxs-lookup"><span data-stu-id="e63c7-183">Method</span></span> | <span data-ttu-id="e63c7-184">說明</span><span class="sxs-lookup"><span data-stu-id="e63c7-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e63c7-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="e63c7-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="e63c7-186">指示 hello 裝置 tooperform 韌體更新</span><span class="sxs-lookup"><span data-stu-id="e63c7-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="e63c7-187">重新啟動</span><span class="sxs-lookup"><span data-stu-id="e63c7-187">Reboot</span></span> |<span data-ttu-id="e63c7-188">指示 hello 裝置 tooreboot</span><span class="sxs-lookup"><span data-stu-id="e63c7-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="e63c7-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="e63c7-189">FactoryReset</span></span> |<span data-ttu-id="e63c7-190">指示 hello 裝置 tooperform 原廠重設</span><span class="sxs-lookup"><span data-stu-id="e63c7-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="e63c7-191">有些方法會使用進度報告的內容 tooreport。</span><span class="sxs-lookup"><span data-stu-id="e63c7-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="e63c7-192">例如，hello **InitiateFirmwareUpdate**方法模擬 hello 裝置上以非同步方式執行 hello 更新。</span><span class="sxs-lookup"><span data-stu-id="e63c7-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="e63c7-193">hello 方法會立即傳回 hello 在裝置上，同時 hello 非同步工作會繼續 toosend 狀態更新回 toohello 方案儀表板中使用報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="e63c7-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="e63c7-194">命令</span><span class="sxs-lookup"><span data-stu-id="e63c7-194">Commands</span></span>

<span data-ttu-id="e63c7-195">hello 模擬裝置可以處理下列命令 （雲端到裝置訊息） 從 hello 方案入口網站來完成 hello IoT 中樞傳送的 hello:</span><span class="sxs-lookup"><span data-stu-id="e63c7-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="e63c7-196">命令</span><span class="sxs-lookup"><span data-stu-id="e63c7-196">Command</span></span> | <span data-ttu-id="e63c7-197">說明</span><span class="sxs-lookup"><span data-stu-id="e63c7-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e63c7-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="e63c7-198">PingDevice</span></span> |<span data-ttu-id="e63c7-199">傳送*ping* toohello 裝置 toocheck 是保持運作</span><span class="sxs-lookup"><span data-stu-id="e63c7-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="e63c7-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="e63c7-200">StartTelemetry</span></span> |<span data-ttu-id="e63c7-201">啟動 hello 裝置傳送遙測</span><span class="sxs-lookup"><span data-stu-id="e63c7-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="e63c7-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="e63c7-202">StopTelemetry</span></span> |<span data-ttu-id="e63c7-203">停駐點 hello 裝置傳送遙測</span><span class="sxs-lookup"><span data-stu-id="e63c7-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="e63c7-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="e63c7-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="e63c7-205">變更 hello 設定點值周圍的 hello 隨機產生的資料</span><span class="sxs-lookup"><span data-stu-id="e63c7-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="e63c7-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="e63c7-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="e63c7-207">觸發程序 hello 裝置模擬器 toosend 其他遙測值 (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="e63c7-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="e63c7-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="e63c7-208">ChangeDeviceState</span></span> |<span data-ttu-id="e63c7-209">變更裝置 hello 擴充的狀態屬性並從 hello 裝置傳送 hello 裝置資訊訊息</span><span class="sxs-lookup"><span data-stu-id="e63c7-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="e63c7-210">如需這些命令 (雲端到裝置訊息) 和方法 (直接方法) 的比較，請參閱[雲端到裝置通訊指引][lnk-c2d-guidance]。</span><span class="sxs-lookup"><span data-stu-id="e63c7-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="e63c7-211">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="e63c7-211">IoT Hub</span></span>

<span data-ttu-id="e63c7-212">hello [IoT 中樞][ lnk-iothub]內嵌到 hello 雲端從 hello 裝置傳送資料，並使其成為可用 toohello Azure 資料流分析 (ASA) 作業。</span><span class="sxs-lookup"><span data-stu-id="e63c7-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="e63c7-213">每個資料流 ASA 工作會使用個別的 IoT 中樞取用者群組 tooread hello 訊息資料流從您的裝置。</span><span class="sxs-lookup"><span data-stu-id="e63c7-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="e63c7-214">也 hello hello 方案中的 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="e63c7-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="e63c7-215">維護儲存 hello 識別碼和驗證金鑰允許 tooconnect toohello 入口網站的所有 hello 裝置身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="e63c7-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="e63c7-216">您可以啟用和停用透過 hello 身分識別登錄的裝置。</span><span class="sxs-lookup"><span data-stu-id="e63c7-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="e63c7-217">命令 tooyour 裝置的身分將傳送嗨方案入口網站。</span><span class="sxs-lookup"><span data-stu-id="e63c7-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="e63c7-218">代表 hello 方案入口網站來叫用您的裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="e63c7-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="e63c7-219">維護所有已註冊裝置的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="e63c7-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="e63c7-220">裝置的兩個儲存報告的裝置 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="e63c7-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="e63c7-221">裝置的兩個也會儲存所需的屬性，在 hello 方案入口網站的 hello 裝置 tooretrieve 接下來連接時設定。</span><span class="sxs-lookup"><span data-stu-id="e63c7-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="e63c7-222">排程工作的多個裝置的 tooset 屬性，或叫用多個裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="e63c7-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="e63c7-223">Azure 串流分析</span><span class="sxs-lookup"><span data-stu-id="e63c7-223">Azure Stream Analytics</span></span>

<span data-ttu-id="e63c7-224">在遠端監視解決方案，hello [Azure Stream Analytics] [ lnk-asa] (ASA) 會將收到 hello IoT 中樞 tooother 後端元件進行處理或儲存體裝置訊息發送。</span><span class="sxs-lookup"><span data-stu-id="e63c7-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="e63c7-225">不同 ASA 工作執行的 hello 訊息 hello 內容為基礎的特定功能。</span><span class="sxs-lookup"><span data-stu-id="e63c7-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="e63c7-226">**工作 1： 裝置資訊**篩選從 hello 內送訊息資料流的裝置資訊訊息，並將它們傳送 tooan 事件中樞端點。</span><span class="sxs-lookup"><span data-stu-id="e63c7-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="e63c7-227">裝置傳送郵件的裝置資訊，在啟動和回應 tooa **SendDeviceInfo**命令。</span><span class="sxs-lookup"><span data-stu-id="e63c7-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="e63c7-228">此工作會使用下列查詢定義 tooidentify hello**裝置資訊**訊息：</span><span class="sxs-lookup"><span data-stu-id="e63c7-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="e63c7-229">這項作業會傳送其輸出 tooan 事件中心的進一步處理。</span><span class="sxs-lookup"><span data-stu-id="e63c7-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="e63c7-230">**作業 2：規則** 會針對每一裝置臨界值評估傳入氣溫和溼度遙測值。</span><span class="sxs-lookup"><span data-stu-id="e63c7-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="e63c7-231">在 hello hello 方案入口網站中提供的規則編輯器中設定臨界值。</span><span class="sxs-lookup"><span data-stu-id="e63c7-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="e63c7-232">每個裝置/值組是依據時間戳記儲存在 blob 中，串流分析會讀取做為 **參考資料**。</span><span class="sxs-lookup"><span data-stu-id="e63c7-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="e63c7-233">hello 工作比較 hello 裝置 hello 設定的閾值對任何非空白的值。</span><span class="sxs-lookup"><span data-stu-id="e63c7-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="e63c7-234">如果它超過 hello ' >' 條件，hello 工作輸出**警示**超過事件，表示該 hello 臨界值，並提供裝置 hello、 值和時間戳記值。</span><span class="sxs-lookup"><span data-stu-id="e63c7-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="e63c7-235">此工作會使用下列查詢定義 tooidentify 遙測訊息應該會觸發警示的 hello:</span><span class="sxs-lookup"><span data-stu-id="e63c7-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="e63c7-236">hello 工作會傳送其輸出 tooan 事件中心的進一步處理，其中 hello 方案入口網站可以讀取 hello 警示資訊會儲存每個警示 tooblob 儲存體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e63c7-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="e63c7-237">**工作 3： 遙測**hello 傳入裝置遙測資料流上兩種方式運作。</span><span class="sxs-lookup"><span data-stu-id="e63c7-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="e63c7-238">hello 第一次傳送遙測的所有訊息從 hello 裝置 toopersistent blob 儲存體進行長期儲存。</span><span class="sxs-lookup"><span data-stu-id="e63c7-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="e63c7-239">hello 第二個計算平均值、 最小值和最大溼度值經過五分鐘滑動視窗，並傳送這個資料 tooblob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e63c7-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="e63c7-240">hello 方案入口網站會讀取 blob 儲存體 toopopulate hello 圖表中的 hello 遙測資料。</span><span class="sxs-lookup"><span data-stu-id="e63c7-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="e63c7-241">此工作會使用下列查詢定義的 hello:</span><span class="sxs-lookup"><span data-stu-id="e63c7-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="e63c7-242">事件中樞</span><span class="sxs-lookup"><span data-stu-id="e63c7-242">Event Hubs</span></span>

<span data-ttu-id="e63c7-243">hello**裝置資訊**和**規則**ASA 工作輸出及其資料 tooEvent 集線器 tooreliably 向前上 toohello**事件處理器**hello WebJob 中執行。</span><span class="sxs-lookup"><span data-stu-id="e63c7-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="e63c7-244">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63c7-244">Azure storage</span></span>

<span data-ttu-id="e63c7-245">hello 解決方案會使用 Azure blob 儲存體 toopersist 所有 hello 原始和摘要遙測資料從 hello 裝置 hello 方案中。</span><span class="sxs-lookup"><span data-stu-id="e63c7-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="e63c7-246">hello 入口網站會讀取 blob 儲存體 toopopulate hello 圖表中的 hello 遙測資料。</span><span class="sxs-lookup"><span data-stu-id="e63c7-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="e63c7-247">toodisplay 警示 hello 方案入口網站，讀取 hello blob 儲存體記錄的遙測值超過 hello 設定臨界值時。</span><span class="sxs-lookup"><span data-stu-id="e63c7-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="e63c7-248">hello 解決方案也會使用 blob 儲存體 toorecord hello 臨界值 hello 方案入口網站中設定。</span><span class="sxs-lookup"><span data-stu-id="e63c7-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="e63c7-249">WebJobs</span><span class="sxs-lookup"><span data-stu-id="e63c7-249">WebJobs</span></span>

<span data-ttu-id="e63c7-250">此外 toohosting hello 裝置模擬器都會 hello WebJobs hello 方案中也主機 hello**事件處理器**Azure WebJob 會處理命令的回應中執行。</span><span class="sxs-lookup"><span data-stu-id="e63c7-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="e63c7-251">它會使用命令的回應訊息 tooupdate hello 裝置命令歷程記錄 （儲存在 hello Cosmos DB 資料庫）。</span><span class="sxs-lookup"><span data-stu-id="e63c7-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="e63c7-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e63c7-252">Cosmos DB</span></span>

<span data-ttu-id="e63c7-253">hello 解決方案會使用 Cosmos DB 資料庫 toostore 需 hello 裝置連線的 toohello 解決方案資訊。</span><span class="sxs-lookup"><span data-stu-id="e63c7-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="e63c7-254">這項資訊包括 hello 歷程記錄從 hello 方案入口網站傳送 toodevices 命令和叫用從 hello 方案入口網站的方法。</span><span class="sxs-lookup"><span data-stu-id="e63c7-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="e63c7-255">解決方案入口網站</span><span class="sxs-lookup"><span data-stu-id="e63c7-255">Solution portal</span></span>

<span data-ttu-id="e63c7-256">hello 方案入口網站是 web 應用程式部署成預先設定的 hello 方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="e63c7-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="e63c7-257">hello 方案入口網站中的 hello 金鑰頁面是 hello 儀表板和 hello 裝置清單。</span><span class="sxs-lookup"><span data-stu-id="e63c7-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="e63c7-258">儀表板</span><span class="sxs-lookup"><span data-stu-id="e63c7-258">Dashboard</span></span>

<span data-ttu-id="e63c7-259">此頁面在 hello web 應用程式會使用 PowerBI javascript 控制項 (請參閱[PowerBI 視覺效果儲存機制](https://www.github.com/Microsoft/PowerBI-visuals)) hello 裝置 toovisualize hello 遙測資料。</span><span class="sxs-lookup"><span data-stu-id="e63c7-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="e63c7-260">hello 解決方案會使用 hello ASA 遙測工作 toowrite hello 遙測資料 tooblob 儲存區。</span><span class="sxs-lookup"><span data-stu-id="e63c7-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="e63c7-261">裝置清單</span><span class="sxs-lookup"><span data-stu-id="e63c7-261">Device list</span></span>

<span data-ttu-id="e63c7-262">您可以從這個頁面在 hello 方案入口網站：</span><span class="sxs-lookup"><span data-stu-id="e63c7-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="e63c7-263">佈建新裝置。</span><span class="sxs-lookup"><span data-stu-id="e63c7-263">Provision a new device.</span></span> <span data-ttu-id="e63c7-264">此動作設定 hello 唯一裝置識別碼，並會產生 hello 驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="e63c7-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="e63c7-265">它會寫入 hello 裝置 tooboth hello IoT 中樞身分識別登錄的相關資訊與 hello 解決方案專用 Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e63c7-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="e63c7-266">管理裝置屬性。</span><span class="sxs-lookup"><span data-stu-id="e63c7-266">Manage device properties.</span></span> <span data-ttu-id="e63c7-267">這個動作包括檢視現有屬性和使用新的屬性更新。</span><span class="sxs-lookup"><span data-stu-id="e63c7-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="e63c7-268">傳送命令 tooa 裝置。</span><span class="sxs-lookup"><span data-stu-id="e63c7-268">Send commands tooa device.</span></span>
* <span data-ttu-id="e63c7-269">檢視裝置 hello 命令歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="e63c7-269">View hello command history for a device.</span></span>
* <span data-ttu-id="e63c7-270">啟用和停用裝置。</span><span class="sxs-lookup"><span data-stu-id="e63c7-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e63c7-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e63c7-271">Next steps</span></span>

<span data-ttu-id="e63c7-272">hello 下列 TechNet 部落格文章提供更多詳細 hello 遠端監視預先設定的解決方案：</span><span class="sxs-lookup"><span data-stu-id="e63c7-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="e63c7-273">IoT 套件下 hello 其實-遠端監視</span><span class="sxs-lookup"><span data-stu-id="e63c7-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="e63c7-274">IoT 套件 - 遠端監視 - 新增即時與模擬裝置</span><span class="sxs-lookup"><span data-stu-id="e63c7-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="e63c7-275">您可以繼續閱讀下列文章 hello 入門 IoT 套件：</span><span class="sxs-lookup"><span data-stu-id="e63c7-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="e63c7-276">[連接您的裝置 toohello 遠端監視預先設定的解決方案][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="e63c7-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="e63c7-277">[Hello azureiotsuite.com 網站的權限][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="e63c7-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
