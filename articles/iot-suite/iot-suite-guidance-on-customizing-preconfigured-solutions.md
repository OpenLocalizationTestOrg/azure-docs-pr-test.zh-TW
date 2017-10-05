---
title: "自訂預先設定解決方案 | Microsoft Docs"
description: "提供如何自訂 Azure IoT 套件預先設定解決方案的指引。"
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
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="dbbda-103">自訂預先設定的方案</span><span class="sxs-lookup"><span data-stu-id="dbbda-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="dbbda-104">Azure IoT Suite 提供的預先設定解決方案能夠示範套件中共同運作的服務可提供端對端解決方案。</span><span class="sxs-lookup"><span data-stu-id="dbbda-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="dbbda-105">從這裡開始，有多個不同地方可以擴充並針對特定案例自訂解決方案。</span><span class="sxs-lookup"><span data-stu-id="dbbda-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="dbbda-106">下列各節說明這些常見的自訂點。</span><span class="sxs-lookup"><span data-stu-id="dbbda-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="dbbda-107">尋找原始程式碼</span><span class="sxs-lookup"><span data-stu-id="dbbda-107">Find the source code</span></span>

<span data-ttu-id="dbbda-108">預先設定解決方案的原始程式碼可在以下 GitHub 的儲存機制取得：</span><span class="sxs-lookup"><span data-stu-id="dbbda-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="dbbda-109">遠端監視： [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="dbbda-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="dbbda-110">預測性維護︰ [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="dbbda-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="dbbda-111">已連線的處理站︰[https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="dbbda-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="dbbda-112">提供預先設定解決方案原始程式碼的目的，在於示範實作使用 Azure IoT 套件之 IoT 解決方案的端對端功能時，所採用的模式和作法。</span><span class="sxs-lookup"><span data-stu-id="dbbda-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="dbbda-113">您可以找到如何在 GitHub 儲存機制中建置和部署解決方案的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dbbda-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="dbbda-114">變更預先設定的規則</span><span class="sxs-lookup"><span data-stu-id="dbbda-114">Change the preconfigured rules</span></span>

<span data-ttu-id="dbbda-115">遠端監視解決方案包含三個 [Azure 串流分析](https://azure.microsoft.com/services/stream-analytics/)作業，這些作業可處理解決方案中的裝置資訊、遙測及規則邏輯。</span><span class="sxs-lookup"><span data-stu-id="dbbda-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="dbbda-116">[遠端監視預先設定解決方案逐步解說](iot-suite-remote-monitoring-sample-walkthrough.md)提供這三個串流分析作業和其語法的深入描述。</span><span class="sxs-lookup"><span data-stu-id="dbbda-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="dbbda-117">您可以直接編輯這些工作以改變邏輯，或新增案例特有的邏輯。</span><span class="sxs-lookup"><span data-stu-id="dbbda-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="dbbda-118">您可以尋找串流分析工作，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="dbbda-119">移至 [[Azure 入口網站] ](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="dbbda-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dbbda-120">瀏覽至名稱與 IoT 解決方案相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="dbbda-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="dbbda-121">選取要修改的 Azure 串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="dbbda-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="dbbda-122">在命令集中選取 [停止] 以停止作業。</span><span class="sxs-lookup"><span data-stu-id="dbbda-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="dbbda-123">編輯輸入、查詢及輸出。</span><span class="sxs-lookup"><span data-stu-id="dbbda-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="dbbda-124">簡單修改的目的在於變更**規則**作業的查詢，以便使用 **"<"** 而不是 **">"**。</span><span class="sxs-lookup"><span data-stu-id="dbbda-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="dbbda-125">編輯規則時，解決方案入口網站仍會顯示 **">"**，不過因為基礎作業中的變更，您可以發現行為已翻轉。</span><span class="sxs-lookup"><span data-stu-id="dbbda-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="dbbda-126">啟動工作</span><span class="sxs-lookup"><span data-stu-id="dbbda-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="dbbda-127">遠端監視儀表板依賴特定資料，因此變更工作可能會造成儀表板失敗。</span><span class="sxs-lookup"><span data-stu-id="dbbda-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="dbbda-128">新增自己的規則</span><span class="sxs-lookup"><span data-stu-id="dbbda-128">Add your own rules</span></span>

<span data-ttu-id="dbbda-129">除了變更預先設定的 Azure 串流分析工作，您也可以使用 Azure 入口網站新增工作或新增現有工作的查詢。</span><span class="sxs-lookup"><span data-stu-id="dbbda-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="dbbda-130">自訂裝置</span><span class="sxs-lookup"><span data-stu-id="dbbda-130">Customize devices</span></span>

<span data-ttu-id="dbbda-131">最常見的擴充功能活動之一是使用案例特定的裝置。</span><span class="sxs-lookup"><span data-stu-id="dbbda-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="dbbda-132">使用裝置的方法有數種。</span><span class="sxs-lookup"><span data-stu-id="dbbda-132">There are several methods for working with devices.</span></span> <span data-ttu-id="dbbda-133">這些方法包括變更模擬裝置以符合您的案例，或使用 [IoT Device SDK][IoT Device SDK] 將實體裝置連接到解決方案。</span><span class="sxs-lookup"><span data-stu-id="dbbda-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="dbbda-134">如需新增裝置的逐步指南，請參閱 [Iot 套件連接裝置](iot-suite-connecting-devices.md)一文和[遠端監視 C SDK 範例](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring)。</span><span class="sxs-lookup"><span data-stu-id="dbbda-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="dbbda-135">此範例設計用於搭配預先設定的遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="dbbda-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="dbbda-136">建立自己的模擬裝置</span><span class="sxs-lookup"><span data-stu-id="dbbda-136">Create your own simulated device</span></span>

<span data-ttu-id="dbbda-137">[遠端監視解決方案原始程式碼](https://github.com/Azure/azure-iot-remote-monitoring)中包含 .NET 模擬器。</span><span class="sxs-lookup"><span data-stu-id="dbbda-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="dbbda-138">此模擬器是解決方案中佈建的模擬器，您可加以變更，以傳送不同的中繼資料、遙測，以及回應不同的命令和方法。</span><span class="sxs-lookup"><span data-stu-id="dbbda-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="dbbda-139">預先設定的遠端監視解決方案中預先設定的模擬器會模擬可發出溫度和濕度遙測的冷卻裝置。</span><span class="sxs-lookup"><span data-stu-id="dbbda-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="dbbda-140">當您分接 GitHub 儲存機制後，可以在 [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) 專案中修改模擬器。</span><span class="sxs-lookup"><span data-stu-id="dbbda-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="dbbda-141">模擬裝置的可用位置</span><span class="sxs-lookup"><span data-stu-id="dbbda-141">Available locations for simulated devices</span></span>

<span data-ttu-id="dbbda-142">預設的一組位置是在美國華盛頓州的西雅圖市/雷德蒙德市。</span><span class="sxs-lookup"><span data-stu-id="dbbda-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="dbbda-143">您可以在 [SampleDeviceFactory.cs][lnk-sample-device-factory] 變更這些位置。</span><span class="sxs-lookup"><span data-stu-id="dbbda-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="dbbda-144">將所需屬性更新處理常式新增至模擬器</span><span class="sxs-lookup"><span data-stu-id="dbbda-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="dbbda-145">您可以在解決方案入口網站中設定裝置的所需屬性值。</span><span class="sxs-lookup"><span data-stu-id="dbbda-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="dbbda-146">當裝置擷取所需屬性值，裝置必須處理屬性變更要求。</span><span class="sxs-lookup"><span data-stu-id="dbbda-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="dbbda-147">若要透過所需屬性新增屬性值變更支援，您需要將處理常式新增至模擬器。</span><span class="sxs-lookup"><span data-stu-id="dbbda-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="dbbda-148">此模擬器包含 **SetPointTemp** 和 **TelemetryInterval** 屬性的處理常式，而您可以在解決方案入口網站中設定這些屬性的所需值來加以更新。</span><span class="sxs-lookup"><span data-stu-id="dbbda-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="dbbda-149">下列範例顯示 **CoolerDevice** 類別中 **SetPointTemp** 所要屬性的處理常式︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="dbbda-150">這個方法會更新遙測點溫度，然後藉由設定報告屬性向 IoT 中樞回報變更。</span><span class="sxs-lookup"><span data-stu-id="dbbda-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="dbbda-151">您可以依照上述範例中的模式，為自己的屬性新增自己的處理常式。</span><span class="sxs-lookup"><span data-stu-id="dbbda-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="dbbda-152">您也必須將所需屬性從 **CoolerDevice** 建構函式繫結至如下列範例所示的處理常式︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="dbbda-153">請注意，**SetPointTempPropertyName** 是定義為 "Config.SetPointTemp" 的常數。</span><span class="sxs-lookup"><span data-stu-id="dbbda-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="dbbda-154">將新方法支援新增至模擬器</span><span class="sxs-lookup"><span data-stu-id="dbbda-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="dbbda-155">您可以自訂模擬器，以新增[方法 (直接方法)][lnk-direct-methods] 支援。</span><span class="sxs-lookup"><span data-stu-id="dbbda-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="dbbda-156">有兩個必備主要步驟︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-156">There are two key steps required:</span></span>

- <span data-ttu-id="dbbda-157">模擬器必須將方法的詳細資料告知預先設定之解決方案中的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dbbda-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="dbbda-158">模擬器必須包含程式碼，以便在您從解決方案總管的 [裝置詳細資料] 面板或透過作業叫用方法時，處理方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="dbbda-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="dbbda-159">預先設定的遠端監視解決方案會使用*報告屬性*，將所支援方法的詳細資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dbbda-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="dbbda-160">解決方案後端會維護每個裝置支援的所有方法清單，以及方法引動過程的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="dbbda-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="dbbda-161">您可以檢視有關裝置的這項資訊，並且在解決方案入口網站中叫用方法。</span><span class="sxs-lookup"><span data-stu-id="dbbda-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="dbbda-162">若要通知 IoT 中樞，裝置可支援某種方法，裝置必須將此方法的詳細資訊新增至報告屬性中的 **SupportedMethods** 節點︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="dbbda-163">方法簽章具有下列格式︰`<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`。</span><span class="sxs-lookup"><span data-stu-id="dbbda-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="dbbda-164">例如，若要指定預期有名為 **FwPackageURI** 之字串參數的 **InitiateFirmwareUpdate** 方法，請使用下列方法簽章︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="dbbda-165">如需支援的參數類型清單，請參閱 Infrastructure 專案中的 **CommandTypes** 類別。</span><span class="sxs-lookup"><span data-stu-id="dbbda-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="dbbda-166">若要刪除方法，將報告屬性中的方法簽章設定為 `null`。</span><span class="sxs-lookup"><span data-stu-id="dbbda-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="dbbda-167">當解決方案後端從裝置收到「裝置資訊」訊息時，只會更新所支援方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="dbbda-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="dbbda-168">下列來自 Common 專案中 **SampleDeviceFactory** 類別的程式碼範例示範如何將方法新增至裝置所傳送之報告屬性的 **SupportedMethods** 清單：</span><span class="sxs-lookup"><span data-stu-id="dbbda-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="dbbda-169">此程式碼片段會新增 **InitiateFirmwareUpdate** 方法的詳細資料，包括要在解決方案入口網站中顯示的文字以及所需方法參數的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dbbda-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="dbbda-170">模擬器會在啟動時將報告屬性 (包括支援的方法清單) 傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dbbda-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="dbbda-171">針對模擬器支援的每個方法，將處理常式新增至模擬器程式碼。</span><span class="sxs-lookup"><span data-stu-id="dbbda-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="dbbda-172">您可以在 Simulator.WebJob 專案的 **CoolerDevice** 類別中看到現有的處理常式。</span><span class="sxs-lookup"><span data-stu-id="dbbda-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="dbbda-173">下列範例顯示 **InitiateFirmwareUpdate** 方法的處理常式︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="dbbda-174">方法處理常式名稱的開頭必須是 `On` 後面加上方法名稱。</span><span class="sxs-lookup"><span data-stu-id="dbbda-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="dbbda-175">**MethodRequest** 參數包含從解決方案後端叫用方法時所傳遞的任何參數。</span><span class="sxs-lookup"><span data-stu-id="dbbda-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="dbbda-176">傳回值的類型必須是 **Task&lt;MethodResponse&gt;**。</span><span class="sxs-lookup"><span data-stu-id="dbbda-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="dbbda-177">**BuildMethodResponse** 公用程式方法可協助您建立傳回值。</span><span class="sxs-lookup"><span data-stu-id="dbbda-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="dbbda-178">在方法處理常式中，您可以︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="dbbda-179">啟動非同步工作。</span><span class="sxs-lookup"><span data-stu-id="dbbda-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="dbbda-180">從 IoT 中樞的*裝置對應項*擷取所需屬性。</span><span class="sxs-lookup"><span data-stu-id="dbbda-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="dbbda-181">使用 **CoolerDevice** 類別中的 **SetReportedPropertyAsync** 方法，更新單一報告屬性。</span><span class="sxs-lookup"><span data-stu-id="dbbda-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="dbbda-182">建立 **TwinCollection** 執行個體並呼叫 **Transport.UpdateReportedPropertiesAsync** 方法，以更新多個報告屬性。</span><span class="sxs-lookup"><span data-stu-id="dbbda-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="dbbda-183">先前的韌體更新範例會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dbbda-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="dbbda-184">檢查裝置能夠接受韌體更新要求。</span><span class="sxs-lookup"><span data-stu-id="dbbda-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="dbbda-185">以非同步方式起始韌體更新作業，並在作業完成時重設遙測。</span><span class="sxs-lookup"><span data-stu-id="dbbda-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="dbbda-186">立即傳回「已接受 FirmwareUpdate」訊息，表示裝置已接受此要求。</span><span class="sxs-lookup"><span data-stu-id="dbbda-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="dbbda-187">建置並使用自己的 (實體) 裝置</span><span class="sxs-lookup"><span data-stu-id="dbbda-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="dbbda-188">[Azure IoT SDK](https://github.com/Azure/azure-iot-sdks) 提供用來將各種裝置類型 (語言和作業系統) 連接至 IoT 解決方案中的程式庫。</span><span class="sxs-lookup"><span data-stu-id="dbbda-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="dbbda-189">修改儀表板限制</span><span class="sxs-lookup"><span data-stu-id="dbbda-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="dbbda-190">儀表板下拉式清單中顯示的裝置數目</span><span class="sxs-lookup"><span data-stu-id="dbbda-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="dbbda-191">預設值為 200。</span><span class="sxs-lookup"><span data-stu-id="dbbda-191">The default is 200.</span></span> <span data-ttu-id="dbbda-192">您可以在 [DashboardController.cs][lnk-dashboard-controller] 變更這個數字。</span><span class="sxs-lookup"><span data-stu-id="dbbda-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="dbbda-193">Bing 地圖控制項中要顯示的釘選數目</span><span class="sxs-lookup"><span data-stu-id="dbbda-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="dbbda-194">預設值為 200。</span><span class="sxs-lookup"><span data-stu-id="dbbda-194">The default is 200.</span></span> <span data-ttu-id="dbbda-195">您可以在 [TelemetryApiController.cs][lnk-telemetry-api-controller-01] 變更這個數字。</span><span class="sxs-lookup"><span data-stu-id="dbbda-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="dbbda-196">遙測圖形的期間</span><span class="sxs-lookup"><span data-stu-id="dbbda-196">Time period of telemetry graph</span></span>

<span data-ttu-id="dbbda-197">預設值是 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="dbbda-197">The default is 10 minutes.</span></span> <span data-ttu-id="dbbda-198">您可以在 [TelmetryApiController.cs][lnk-telemetry-api-controller-02] 變更此值。</span><span class="sxs-lookup"><span data-stu-id="dbbda-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="dbbda-199">手動設定應用程式角色</span><span class="sxs-lookup"><span data-stu-id="dbbda-199">Manually set up application roles</span></span>

<span data-ttu-id="dbbda-200">以下程序描述如何將 **Admin** 和 **ReadOnly** 應用程式角色新增至預先設定的解決方案中。</span><span class="sxs-lookup"><span data-stu-id="dbbda-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="dbbda-201">請注意，從 azureiotsuite.com 網站佈建的預先設定解決方案已經包含 **Admin** 和 **ReadOnly** 角色。</span><span class="sxs-lookup"><span data-stu-id="dbbda-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="dbbda-202">**ReadOnly** 角色的成員可以看到儀表板和裝置清單，但不能加入裝置、變更裝置屬性或傳送命令。</span><span class="sxs-lookup"><span data-stu-id="dbbda-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="dbbda-203">**Admin** 角色的成員具有解決方案中所有功能的完整存取權。</span><span class="sxs-lookup"><span data-stu-id="dbbda-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="dbbda-204">前往 [Azure 傳統入口網站][lnk-classic-portal]。</span><span class="sxs-lookup"><span data-stu-id="dbbda-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="dbbda-205">選取 **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="dbbda-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="dbbda-206">按一下您在佈建解決方案時所使用的 AAD 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="dbbda-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="dbbda-207">按一下 [應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="dbbda-207">Click **Applications**.</span></span>
5. <span data-ttu-id="dbbda-208">按一下符合預先設定之方案名稱的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="dbbda-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="dbbda-209">如果清單中看不到您的應用程式，請選取 [顯示] 下拉式清單中的 [我公司所擁有的應用程式]，然後按一下核取記號。</span><span class="sxs-lookup"><span data-stu-id="dbbda-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="dbbda-210">在頁面底部，按一下 [管理資訊清單]，然後按一下 [下載資訊清單]。</span><span class="sxs-lookup"><span data-stu-id="dbbda-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="dbbda-211">這個程序會將 .json 檔案下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="dbbda-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="dbbda-212">使用您選擇的文字編輯器開啟此檔案並加以編輯。</span><span class="sxs-lookup"><span data-stu-id="dbbda-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="dbbda-213">在 .json 檔案的第三行，您會看到︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="dbbda-214">使用以下程式碼來取代這一行：</span><span class="sxs-lookup"><span data-stu-id="dbbda-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="dbbda-215">儲存更新後的.json 檔案 (可以覆寫現有的檔案)。</span><span class="sxs-lookup"><span data-stu-id="dbbda-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="dbbda-216">在 Azure 傳統入口網站中，選取頁面底部的 [管理資訊清單]，然後選取 [上傳資訊清單] 上傳您在上一個步驟儲存的 .json 檔案。</span><span class="sxs-lookup"><span data-stu-id="dbbda-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="dbbda-217">您現在已為您的應用程式新增 **Admin** 和 **ReadOnly** 角色。</span><span class="sxs-lookup"><span data-stu-id="dbbda-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="dbbda-218">若要將其中一個角色指派給您目錄中的使用者，請參閱 [azureiotsuite.com 網站的權限][lnk-permissions]。</span><span class="sxs-lookup"><span data-stu-id="dbbda-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="dbbda-219">意見反應</span><span class="sxs-lookup"><span data-stu-id="dbbda-219">Feedback</span></span>

<span data-ttu-id="dbbda-220">本文件是否涵蓋您感興趣的自訂內容？</span><span class="sxs-lookup"><span data-stu-id="dbbda-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="dbbda-221">請在 [User Voice (使用者心聲)](https://feedback.azure.com/forums/321918-azure-iot) 中加入功能建議，或在本文留言。</span><span class="sxs-lookup"><span data-stu-id="dbbda-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dbbda-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dbbda-222">Next steps</span></span>

<span data-ttu-id="dbbda-223">若要深入了解自訂預先設定的解決方案的選項，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="dbbda-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="dbbda-224">[將邏輯應用程式連接至 Azure IoT 套件遠端監視預先設定解決方案][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="dbbda-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="dbbda-225">[搭配使用動態遙測與遠端監視預先設定解決方案][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="dbbda-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="dbbda-226">[遠端監視預先設定方案中的裝置資訊中繼資料][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="dbbda-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="dbbda-227">[自訂連線工廠解決方案顯示 OPC UA 伺服器資料的方式][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="dbbda-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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