---
title: "Azure IoT 中樞作業監視 | Microsoft Docs"
description: "如何使用 Azure IoT 中樞作業監視來即時監視 IoT 中樞上的作業狀態。"
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="d8289-103">IoT 中樞作業監視</span><span class="sxs-lookup"><span data-stu-id="d8289-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="d8289-104">IoT 中樞的作業監視可讓您即時監視其 IoT 中樞上的作業狀態。</span><span class="sxs-lookup"><span data-stu-id="d8289-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="d8289-105">IoT 中樞可追蹤橫跨數個作業類別的事件。</span><span class="sxs-lookup"><span data-stu-id="d8289-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="d8289-106">您可以選擇將一或多個類別的事件傳送至 IoT 中樞的端點進行處理。</span><span class="sxs-lookup"><span data-stu-id="d8289-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="d8289-107">您可以監視資料中是否有錯誤，或根據資料模式設定更複雜的處理行為。</span><span class="sxs-lookup"><span data-stu-id="d8289-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="d8289-108">IoT 中樞會監視六個類別的事件：</span><span class="sxs-lookup"><span data-stu-id="d8289-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="d8289-109">裝置身分識別作業</span><span class="sxs-lookup"><span data-stu-id="d8289-109">Device identity operations</span></span>
* <span data-ttu-id="d8289-110">裝置遙測</span><span class="sxs-lookup"><span data-stu-id="d8289-110">Device telemetry</span></span>
* <span data-ttu-id="d8289-111">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="d8289-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="d8289-112">連線</span><span class="sxs-lookup"><span data-stu-id="d8289-112">Connections</span></span>
* <span data-ttu-id="d8289-113">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="d8289-113">File uploads</span></span>
* <span data-ttu-id="d8289-114">訊息路由</span><span class="sxs-lookup"><span data-stu-id="d8289-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="d8289-115">如何啟用作業監視</span><span class="sxs-lookup"><span data-stu-id="d8289-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="d8289-116">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d8289-116">Create an IoT hub.</span></span> <span data-ttu-id="d8289-117">您可以在[開始使用][lnk-get-started]指南中找到如何建立 IoT 中樞的指示。</span><span class="sxs-lookup"><span data-stu-id="d8289-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="d8289-118">開啟 IoT 中樞的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d8289-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="d8289-119">按一下其中的 [作業監視] 。</span><span class="sxs-lookup"><span data-stu-id="d8289-119">From there, click **Operations monitoring**.</span></span>

    ![在入口網站中存取作業監視組態][1]

1. <span data-ttu-id="d8289-121">選取您要監視的監視類別，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d8289-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="d8289-122">您可以從 [監視設定] 中所列出的事件中樞相容端點讀取事件。</span><span class="sxs-lookup"><span data-stu-id="d8289-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="d8289-123">IoT 中樞端點稱為 `messages/operationsmonitoringevents`。</span><span class="sxs-lookup"><span data-stu-id="d8289-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![在 IoT 中樞上設定作業監視][2]

> [!NOTE]
> <span data-ttu-id="d8289-125">[連線] 類別若選取 [Verbose] 監視，會導致 IoT 中樞產生額外的診斷訊息。</span><span class="sxs-lookup"><span data-stu-id="d8289-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="d8289-126">對於所有其他類別，[Verbose] 設定會變更 IoT 中樞在每個錯誤訊息中包含的資訊量。</span><span class="sxs-lookup"><span data-stu-id="d8289-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="d8289-127">事件類別和其使用方式</span><span class="sxs-lookup"><span data-stu-id="d8289-127">Event categories and how to use them</span></span>

<span data-ttu-id="d8289-128">每個作業監視類別會各自追蹤與 IoT 中樞所進行的不同類型的互動，而每一個監視類別都有結構描述來定義該類別的事件要如何構成。</span><span class="sxs-lookup"><span data-stu-id="d8289-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="d8289-129">裝置身分識別作業</span><span class="sxs-lookup"><span data-stu-id="d8289-129">Device identity operations</span></span>

<span data-ttu-id="d8289-130">裝置身分識別作業類別會追蹤您嘗試在其 IoT 中樞的身分識別登錄中建立、更新或刪除項目時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="d8289-131">佈建案例就很適合追蹤此類別。</span><span class="sxs-lookup"><span data-stu-id="d8289-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="d8289-132">裝置遙測</span><span class="sxs-lookup"><span data-stu-id="d8289-132">Device telemetry</span></span>

<span data-ttu-id="d8289-133">裝置遙測類別會追蹤在 IoT 中樞發生，且與遙測管線相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="d8289-134">此類別包括在傳送遙測事件 (例如節流) 和接收遙測事件 (例如未經授權的讀取器) 時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="d8289-135">這個類別無法捕捉裝置本身所執行之程式碼所造成的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-135">This category cannot catch errors caused by code running on the device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="d8289-136">雲端到裝置的命令</span><span class="sxs-lookup"><span data-stu-id="d8289-136">Cloud-to-device commands</span></span>

<span data-ttu-id="d8289-137">雲端到裝置的命令類別會追蹤在 IoT 中樞發生，且與雲端到裝置訊息管線相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="d8289-138">這個類別包括在傳送雲端到裝置訊息 (例如未經授權的寄件者)、接收雲端到裝置訊息 (例如超過傳遞計數) 和接收雲端到裝置訊息意見反應 (例如意見反應已過期) 時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="d8289-139">如果已成功傳遞雲端到裝置訊息，但裝置未適當處理雲端到裝置訊息，此類別不會捕捉來自此裝置的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="d8289-140">連線</span><span class="sxs-lookup"><span data-stu-id="d8289-140">Connections</span></span>

<span data-ttu-id="d8289-141">連線類別會追蹤當裝置與 IoT 中樞連線或中斷連線時發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="d8289-142">若想識別未經授權的連線嘗試，以及在連線品質不佳之區域內的裝置中斷連線時進行追蹤，就很適合追蹤此類別。</span><span class="sxs-lookup"><span data-stu-id="d8289-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="d8289-143">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="d8289-143">File uploads</span></span>

<span data-ttu-id="d8289-144">檔案上傳類別會追蹤在 IoT 中樞發生且與檔案上傳功能相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="d8289-145">此類別包括︰</span><span class="sxs-lookup"><span data-stu-id="d8289-145">This category includes:</span></span>

* <span data-ttu-id="d8289-146">SAS URI 所發生的錯誤，例如當它在裝置通知中樞已完成上傳之前就到期時。</span><span class="sxs-lookup"><span data-stu-id="d8289-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="d8289-147">裝置所報告的失敗上傳。</span><span class="sxs-lookup"><span data-stu-id="d8289-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="d8289-148">IoT 中樞通知訊息建立期間在儲存體中找不到檔案時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="d8289-149">此類別無法捕捉直接發生在裝置將檔案上傳到儲存體時的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="d8289-150">訊息路由</span><span class="sxs-lookup"><span data-stu-id="d8289-150">Message routing</span></span>

<span data-ttu-id="d8289-151">訊息路由類別會在訊息路由評估期間追蹤發生的錯誤以及 IoT 中樞所認知的端點健全狀況。</span><span class="sxs-lookup"><span data-stu-id="d8289-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="d8289-152">此類別包含的事件像是：當規則評估為「未定義」、當 IoT 中樞將端點標示為無效、及其他任何從端點收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8289-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="d8289-153">此類別不包含有關訊息本身的特定錯誤 (例如裝置節流錯誤)，這些是在「裝置遙測」類別下報告。</span><span class="sxs-lookup"><span data-stu-id="d8289-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="d8289-154">檢視事件</span><span class="sxs-lookup"><span data-stu-id="d8289-154">View events</span></span>

<span data-ttu-id="d8289-155">您可以使用 *iothub-explorer* 工具來快速測試 IoT 中樞正在產生監視事件。</span><span class="sxs-lookup"><span data-stu-id="d8289-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="d8289-156">若要安裝此工具，請參閱 [iothub-explorer][lnk-iothub-explorer] GitHub 儲存機制中的指示。</span><span class="sxs-lookup"><span data-stu-id="d8289-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="d8289-157">請確定入口網站中的 [連線] 監視類別設定為 [詳細資訊]。</span><span class="sxs-lookup"><span data-stu-id="d8289-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="d8289-158">在命令提示字元中，執行下列命令來從監視端點讀取︰</span><span class="sxs-lookup"><span data-stu-id="d8289-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="d8289-159">在另一個命令提示字元中，執行下列命令，以模擬傳送裝置至雲端訊息的裝置︰</span><span class="sxs-lookup"><span data-stu-id="d8289-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="d8289-160">第一個命令提示字元會將監視的事件顯示為連線至您的 IoT 中樞的模擬裝置。</span><span class="sxs-lookup"><span data-stu-id="d8289-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="d8289-161">連線至監視端點</span><span class="sxs-lookup"><span data-stu-id="d8289-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="d8289-162">IoT 中樞上的監視端點是相容於事件中樞的端點。</span><span class="sxs-lookup"><span data-stu-id="d8289-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="d8289-163">您可以使用可搭配「事件中樞」使用的任何機制從此端點讀取監視訊息。</span><span class="sxs-lookup"><span data-stu-id="d8289-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="d8289-164">下列範例會建立的基本讀取器不適合用於高輸送量部署。</span><span class="sxs-lookup"><span data-stu-id="d8289-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="d8289-165">如需有關如何處理來自「事件中樞」之訊息的詳細資訊，請參閱[開始使用事件中樞][lnk-eventhubs-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="d8289-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="d8289-166">若要連線至監視端點，您需要連接字串和端點名稱。</span><span class="sxs-lookup"><span data-stu-id="d8289-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="d8289-167">下列步驟顯示如何在入口網站中尋找需要的值：</span><span class="sxs-lookup"><span data-stu-id="d8289-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="d8289-168">在入口網站中，瀏覽至您的 IoT 中樞資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d8289-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="d8289-169">選擇 [作業監視]，並記下 [事件中樞相容名稱]和 [事件中樞相容端點]值：</span><span class="sxs-lookup"><span data-stu-id="d8289-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![事件中樞相容端點值][img-endpoints]

1. <span data-ttu-id="d8289-171">選擇 [共用存取原則]，然後選擇 [服務]。</span><span class="sxs-lookup"><span data-stu-id="d8289-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="d8289-172">記下**主要金鑰**值：</span><span class="sxs-lookup"><span data-stu-id="d8289-172">Make a note of the **Primary key** value:</span></span>

    ![服務共用存取原則主要金鑰][img-service-key]

<span data-ttu-id="d8289-174">下列 C# 程式碼範例取自 Visual Studio **Windows 傳統桌面** C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8289-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="d8289-175">專案已安裝 **WindowsAzure.ServiceBus** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="d8289-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="d8289-176">以您先前所記下，使用**事件中樞相容端點**和服務**主要金鑰**值的連接字串來取代連接字串預留位置，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d8289-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="d8289-177">以您先前記下的**事件中樞相容名稱**值取代監視端點名稱預留位置。</span><span class="sxs-lookup"><span data-stu-id="d8289-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d8289-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8289-178">Next steps</span></span>
<span data-ttu-id="d8289-179">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="d8289-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d8289-180">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d8289-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d8289-181">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d8289-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md