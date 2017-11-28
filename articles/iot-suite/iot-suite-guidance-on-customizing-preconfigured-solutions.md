---
title: "aaaCustomizing 預先設定的解決方案 |Microsoft 文件"
description: "提供有關如何 toocustomize hello Azure IoT 套件預先設定的解決方案指引。"
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="4a7c9-103">自訂預先設定的方案</span><span class="sxs-lookup"><span data-stu-id="4a7c9-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="4a7c9-104">hello Azure IoT 套件所隨附的預先設定的 hello 解決方案示範 hello 套件工作一起 toodeliver 端對端方案中的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="4a7c9-105">從這個起點，有不同的位置中，您可以擴充和自訂用於特定案例的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="4a7c9-106">hello 下列各節說明這些常見的自訂點。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="4a7c9-107">尋找 hello 原始程式碼</span><span class="sxs-lookup"><span data-stu-id="4a7c9-107">Find hello source code</span></span>

<span data-ttu-id="4a7c9-108">hello 來源的預先設定的 hello 解決方案會提供程式碼在 GitHub 上遵循儲存機制的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a7c9-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="4a7c9-109">遠端監視： [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="4a7c9-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="4a7c9-110">預測性維護︰ [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="4a7c9-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="4a7c9-111">已連線的處理站︰[https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="4a7c9-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="4a7c9-112">toodemonstrate hello 模式和實務用 tooimplement hello 端對端功能的 IoT 解決方案使用 Azure IoT 套件係 hello 原始程式碼 hello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="4a7c9-113">您可以找到更多有關 toobuild 及部署 hello GitHub 儲存機制中的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="4a7c9-114">變更 hello 預先設定規則</span><span class="sxs-lookup"><span data-stu-id="4a7c9-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="4a7c9-115">hello 遠端監視解決方案包括三個[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) toohandle 裝置資訊、 遙測以及在 hello 方案中的規則邏輯的工作。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="4a7c9-116">hello 三個資料流分析工作和其語法所述的 hello 深度[遠端監視預先設定的方案逐步解說](iot-suite-remote-monitoring-sample-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="4a7c9-117">直接 tooalter hello 邏輯，或新增邏輯特定 tooyour 案例中，您可以編輯這些作業。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="4a7c9-118">您可以找到 hello 串流分析工作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="4a7c9-119">跳過[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4a7c9-120">瀏覽以相同的名稱，為您的 IoT 解決方案 hello toohello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="4a7c9-121">選取您想要 toomodify hello Azure Stream Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="4a7c9-122">停止選取的 hello 工作**停止**在 hello 組命令。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="4a7c9-123">編輯 hello 輸入、 查詢和輸出。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="4a7c9-124">簡單的修改是 hello toochange hello 查詢**規則**作業 toouse **"<"**而不是**">"**。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="4a7c9-125">hello 方案入口網站仍會顯示**">"**當您編輯規則，但是請注意 hello 行為翻轉到期 toohello hello 基礎作業變更的方式。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="4a7c9-126">啟動 hello 工作</span><span class="sxs-lookup"><span data-stu-id="4a7c9-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="4a7c9-127">hello 遠端的監視儀表板取決於特定資料，因此改變 hello 作業可能會導致 hello 儀表板 toofail。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="4a7c9-128">新增自己的規則</span><span class="sxs-lookup"><span data-stu-id="4a7c9-128">Add your own rules</span></span>

<span data-ttu-id="4a7c9-129">此外 toochanging hello 預先設定 Azure 串流分析工作，您可以使用 hello Azure 入口網站 tooadd 新作業，或新增新的查詢 tooexisting 工作。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="4a7c9-130">自訂裝置</span><span class="sxs-lookup"><span data-stu-id="4a7c9-130">Customize devices</span></span>

<span data-ttu-id="4a7c9-131">其中一個 hello 最常見的延伸模組活動使用裝置特定 tooyour 案例。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="4a7c9-132">使用裝置的方法有數種。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-132">There are several methods for working with devices.</span></span> <span data-ttu-id="4a7c9-133">這些方法包括變更模擬的裝置 toomatch 案例中，或使用 hello [IoT 裝置 SDK] [ IoT Device SDK] tooconnect 實體裝置 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="4a7c9-134">逐步指南 tooadding 裝置，請參閱 hello [Iot 套件連接裝置](iot-suite-connecting-devices.md)發行項與 hello[遠端監視 sdk > 範例的 C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring)。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="4a7c9-135">這個範例是以 hello 遠端監視預先設定的解決方案設計的 toowork。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="4a7c9-136">建立自己的模擬裝置</span><span class="sxs-lookup"><span data-stu-id="4a7c9-136">Create your own simulated device</span></span>

<span data-ttu-id="4a7c9-137">包含在 hello[遠端監視解決方案原始程式碼](https://github.com/Azure/azure-iot-remote-monitoring)，是.NET 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="4a7c9-138">這個模擬器為 hello 佈建為一部分 hello 方案，而且您可以加以更改 toosend 不同的中繼資料，遙測，並回應 toodifferent 命令和方法的其中一個。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="4a7c9-139">hello 遠端監視預先設定的解決方案中的 hello 預先設定的模擬器模擬冷卻器裝置發出氣溫和溼度的遙測。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="4a7c9-140">您可以修改在 hello hello 模擬器[Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob)專案時，您已分叉 hello GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="4a7c9-141">模擬裝置的可用位置</span><span class="sxs-lookup"><span data-stu-id="4a7c9-141">Available locations for simulated devices</span></span>

<span data-ttu-id="4a7c9-142">西雅圖/Redmond、 Washington、 美國政府正在 hello 預設集合的位置。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="4a7c9-143">您可以在 [SampleDeviceFactory.cs][lnk-sample-device-factory] 變更這些位置。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="4a7c9-144">加入所需的屬性更新處理常式 toohello 模擬器</span><span class="sxs-lookup"><span data-stu-id="4a7c9-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="4a7c9-145">您可以在 hello 方案入口網站中設定裝置所需屬性的值。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="4a7c9-146">它負責 hello hello 裝置 toohandle hello 屬性的變更要求時 hello 裝置擷取所需的 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="4a7c9-147">屬性值變更為 tooadd 支援透過所需的屬性，您需要 tooadd 處理常式 toohello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="4a7c9-148">hello 模擬器包含 hello 的處理常式**SetPointTemp**和**TelemetryInterval**屬性，您可以藉由設定更新預期 hello 方案入口網站中的值。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="4a7c9-149">hello 下列範例顯示 hello 處理常式 hello **SetPointTemp**預期屬性在 hello **CoolerDevice**類別：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="4a7c9-150">這個方法會更新 hello 遙測點溫度，然後報告 hello 變更後 tooIoT 中樞設定報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="4a7c9-151">您可以在 hello 前面範例中的下列 hello 模式所為您自己的屬性加入自己的處理常式。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="4a7c9-152">您也必須繫結 hello 所需的屬性 toohello 處理常式中 hello 下列從 hello 範例所示**CoolerDevice**建構函式：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="4a7c9-153">請注意，**SetPointTempPropertyName** 是定義為 "Config.SetPointTemp" 的常數。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="4a7c9-154">加入新的方法 toohello 模擬器的支援</span><span class="sxs-lookup"><span data-stu-id="4a7c9-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="4a7c9-155">您可以自訂的新 hello 模擬器 tooadd 支援[方法 （直接的方法）][lnk-direct-methods]。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="4a7c9-156">有兩個必備主要步驟︰</span><span class="sxs-lookup"><span data-stu-id="4a7c9-156">There are two key steps required:</span></span>

- <span data-ttu-id="4a7c9-157">hello 模擬器必須通知 hello IoT 中樞 hello 預先設定的方案中使用 hello 方法詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="4a7c9-158">hello 模擬器必須包含程式碼 toohandle hello 方法呼叫，當您叫用它從 hello**裝置詳細資料**hello 方案總管 中，或透過在工作面板。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="4a7c9-159">hello 遠端監視預先設定的解決方案會使用*報告屬性*toosend 的支援的方法 tooIoT 集線器的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="4a7c9-160">hello 方案後端會維護一份所有支援的方法引動過程的歷程記錄以及每個裝置的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="4a7c9-161">您可以檢視此裝置的相關資訊，並叫用 hello 方案入口網站中的方法。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="4a7c9-162">toonotify hello IoT 中樞裝置支援的方法，hello 裝置必須加入詳細資料的 hello 方法 toohello **SupportedMethods** hello 中的節點回報屬性：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="4a7c9-163">hello 方法簽章具有下列格式的 hello: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="4a7c9-164">例如，toospecify hello **InitiateFirmwareUpdate**方法必須要有字串參數名稱為**FwPackageURI**，使用下列方法簽章的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a7c9-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="4a7c9-165">如需支援的參數類型的清單，請參閱 hello **CommandTypes** hello 基礎結構的專案中的類別。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="4a7c9-166">toodelete 方法，設定 hello 方法簽章太`null`hello 中報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="4a7c9-167">hello 方案後端只會更新支援的方法的相關資訊時接收*裝置資訊*從裝置 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="4a7c9-168">下列程式碼範例的 hello hello **SampleDeviceFactory**類別中 hello 通用專案顯示如何 tooadd 方法 toohello 清單的**SupportedMethods** hello 中報告傳送嗨屬性裝置：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="4a7c9-169">此程式碼片段加入詳細資料的 hello **InitiateFirmwareUpdate**包括文字 toodisplay hello 方案入口網站與 hello 的詳細資料的方法所需的方法參數。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="4a7c9-170">hello 模擬器會傳送報告的屬性，包括 hello 的清單支援的方法，tooIoT hello 模擬器啟動時的中樞。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="4a7c9-171">新增支援每個方法的處理常式 toohello 模擬器程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="4a7c9-172">您可以看到 hello hello 中的現有處理常式**CoolerDevice** hello Simulator.WebJob 專案中的類別。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="4a7c9-173">hello 下列範例顯示 hello 處理常式**InitiateFirmwareUpdate**方法：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="4a7c9-174">方法的處理常式名稱開頭必須`On`後面接著 hello hello 方法名稱。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="4a7c9-175">hello **methodRequest**參數會包含從 hello 方案後端以 hello 方法引動過程傳遞任何參數。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="4a7c9-176">hello 傳回值必須是型別**工作&lt;MethodResponse&gt;**。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="4a7c9-177">hello **BuildMethodResponse**公用程式方法，可協助您建立 hello 傳回值。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="4a7c9-178">內部 hello 方法處理常式，您可以：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="4a7c9-179">啟動非同步工作。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="4a7c9-180">擷取所需的屬性從 hello*裝置兩個*在 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="4a7c9-181">更新單一報告的屬性使用 hello **SetReportedPropertyAsync**方法在 hello **CoolerDevice**類別。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="4a7c9-182">更新多個報告的屬性，藉由建立**TwinCollection**執行個體及呼叫 hello **Transport.UpdateReportedPropertiesAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="4a7c9-183">hello 前例的韌體更新會執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a7c9-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="4a7c9-184">檢查 hello 裝置是無法 tooaccept hello 韌體更新要求。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="4a7c9-185">以非同步方式起始 hello 韌體更新作業，而且 hello 作業完成時，會重設 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="4a7c9-186">立即傳回 hello"FirmwareUpdate 接受 」 訊息 tooindicate hello 要求接受 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="4a7c9-187">建置並使用自己的 (實體) 裝置</span><span class="sxs-lookup"><span data-stu-id="4a7c9-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="4a7c9-188">hello [Azure IoT Sdk](https://github.com/Azure/azure-iot-sdks) IoT 解決方案，提供用於連接多個裝置類型 （語言和作業系統） 的程式庫。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="4a7c9-189">修改儀表板限制</span><span class="sxs-lookup"><span data-stu-id="4a7c9-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="4a7c9-190">儀表板下拉式清單中顯示的裝置數目</span><span class="sxs-lookup"><span data-stu-id="4a7c9-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="4a7c9-191">hello 預設值為 200。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-191">hello default is 200.</span></span> <span data-ttu-id="4a7c9-192">您可以在 [DashboardController.cs][lnk-dashboard-controller] 變更這個數字。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="4a7c9-193">在 Bing 地圖控制項中的 pin toodisplay 的數目</span><span class="sxs-lookup"><span data-stu-id="4a7c9-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="4a7c9-194">hello 預設值為 200。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-194">hello default is 200.</span></span> <span data-ttu-id="4a7c9-195">您可以在 [TelemetryApiController.cs][lnk-telemetry-api-controller-01] 變更這個數字。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="4a7c9-196">遙測圖形的期間</span><span class="sxs-lookup"><span data-stu-id="4a7c9-196">Time period of telemetry graph</span></span>

<span data-ttu-id="4a7c9-197">hello 預設值為 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-197">hello default is 10 minutes.</span></span> <span data-ttu-id="4a7c9-198">您可以在 [TelmetryApiController.cs][lnk-telemetry-api-controller-02] 變更此值。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="4a7c9-199">手動設定應用程式角色</span><span class="sxs-lookup"><span data-stu-id="4a7c9-199">Manually set up application roles</span></span>

<span data-ttu-id="4a7c9-200">hello 下列程序描述如何 tooadd **Admin**和**ReadOnly**應用程式角色 tooa 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="4a7c9-201">請注意，佈建 hello azureiotsuite.com 站台已預先設定的解決方案包括 hello **Admin**和**ReadOnly**角色。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="4a7c9-202">成員的 hello **ReadOnly**角色可以看到 hello 儀表板和 hello 裝置清單中，但不是允許有 tooadd 裝置、 變更裝置的屬性或傳送命令。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="4a7c9-203">成員的 hello **Admin**角色擁有完整存取 tooall hello 功能 hello 方案中。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="4a7c9-204">移 toohello [Azure 傳統入口網站][lnk-classic-portal]。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="4a7c9-205">選取 **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="4a7c9-206">按一下 hello 您佈建您的方案時所使用的 hello AAD 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="4a7c9-207">按一下 [應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-207">Click **Applications**.</span></span>
5. <span data-ttu-id="4a7c9-208">按一下 hello 符合預先設定的方案名稱 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="4a7c9-209">如果您沒有看到您的應用程式，在 [hello] 清單中，選取**我公司所擁有的應用程式**在 hello**顯示**下拉式清單中，然後按一下 hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="4a7c9-210">在 hello hello 頁面底部，按一下**管理資訊清單**然後**下載資訊清單**。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="4a7c9-211">此程序下載.json 檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="4a7c9-212">使用您選擇的文字編輯器開啟此檔案並加以編輯。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="4a7c9-213">在 hello.json 檔案 hello 第三行，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="4a7c9-214">這一行取代為下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a7c9-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="4a7c9-215">儲存 hello 更新的.json 檔案 （您可以覆寫現有檔案的 hello）。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="4a7c9-216">在 hello Azure 傳統入口網站底部 hello hello 頁面上，選取 **管理資訊清單**然後**上傳資訊清單**tooupload hello 上一個步驟中儲存的 hello.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="4a7c9-217">您現在已新增 hello **Admin**和**ReadOnly**角色 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="4a7c9-218">其中一個在您目錄中，這些角色 tooa 使用者 tooassign 看到[hello azureiotsuite.com 網站的權限][lnk-permissions]。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="4a7c9-219">意見反應</span><span class="sxs-lookup"><span data-stu-id="4a7c9-219">Feedback</span></span>

<span data-ttu-id="4a7c9-220">您有的自訂，您希望本文件涵蓋的 toosee 嗎？</span><span class="sxs-lookup"><span data-stu-id="4a7c9-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="4a7c9-221">新增功能建議太[User Voice](https://feedback.azure.com/forums/321918-azure-iot)，或針對本文的註解。</span><span class="sxs-lookup"><span data-stu-id="4a7c9-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a7c9-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a7c9-222">Next steps</span></span>

<span data-ttu-id="4a7c9-223">toolearn 進一步了解 hello 選項自訂 hello 預先設定的解決方案，請參閱：</span><span class="sxs-lookup"><span data-stu-id="4a7c9-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="4a7c9-224">[連接邏輯應用程式 tooyour Azure IoT 套件遠端監視預先設定的解決方案][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="4a7c9-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="4a7c9-225">[使用動態遙測以 hello 遠端監視預先設定的解決方案][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="4a7c9-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="4a7c9-226">[裝置資訊的中繼資料中 hello 遠端監視預先設定的解決方案][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="4a7c9-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="4a7c9-227">[自訂 hello 從 OPC UA 伺服器所連接的原廠方案顯示資料][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="4a7c9-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md