---
title: "監視 aaaAzure IoT 中樞作業 |Microsoft 文件"
description: "如何監視 toomonitor toouse Azure IoT 中樞作業 hello 您即時的 IoT 中樞上的作業狀態。"
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
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="d007d-103">IoT 中樞作業監視</span><span class="sxs-lookup"><span data-stu-id="d007d-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="d007d-104">IoT 中樞作業監視可讓您即時您 IoT 中樞上的作業 toomonitor hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="d007d-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="d007d-105">IoT 中樞可追蹤橫跨數個作業類別的事件。</span><span class="sxs-lookup"><span data-stu-id="d007d-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="d007d-106">您可以選擇從您的 IoT 中樞進行處理的一或多個類別 tooan 端點傳送的事件。</span><span class="sxs-lookup"><span data-stu-id="d007d-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="d007d-107">您可以監視有錯誤的 hello 資料或設定根據資料模式更複雜的處理。</span><span class="sxs-lookup"><span data-stu-id="d007d-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="d007d-108">IoT 中樞會監視六個類別的事件：</span><span class="sxs-lookup"><span data-stu-id="d007d-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="d007d-109">裝置身分識別作業</span><span class="sxs-lookup"><span data-stu-id="d007d-109">Device identity operations</span></span>
* <span data-ttu-id="d007d-110">裝置遙測</span><span class="sxs-lookup"><span data-stu-id="d007d-110">Device telemetry</span></span>
* <span data-ttu-id="d007d-111">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="d007d-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="d007d-112">連線</span><span class="sxs-lookup"><span data-stu-id="d007d-112">Connections</span></span>
* <span data-ttu-id="d007d-113">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="d007d-113">File uploads</span></span>
* <span data-ttu-id="d007d-114">訊息路由</span><span class="sxs-lookup"><span data-stu-id="d007d-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="d007d-115">如何 tooenable 作業監視</span><span class="sxs-lookup"><span data-stu-id="d007d-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="d007d-116">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d007d-116">Create an IoT hub.</span></span> <span data-ttu-id="d007d-117">您可以找到指示如何 toocreate hello IoT 中樞[開始][ lnk-get-started]指南。</span><span class="sxs-lookup"><span data-stu-id="d007d-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="d007d-118">開啟您的 IoT 中樞的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d007d-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="d007d-119">按一下其中的 [作業監視] 。</span><span class="sxs-lookup"><span data-stu-id="d007d-119">From there, click **Operations monitoring**.</span></span>

    ![監視 hello 入口網站中的設定的存取作業][1]

1. <span data-ttu-id="d007d-121">監視您希望 toomonitor，，然後按一下類別目錄選取 hello**儲存**。</span><span class="sxs-lookup"><span data-stu-id="d007d-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="d007d-122">hello 事件可用來讀取 hello 事件中樞相容端點中所列**監視設定**。</span><span class="sxs-lookup"><span data-stu-id="d007d-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="d007d-123">hello IoT 中樞端點稱為`messages/operationsmonitoringevents`。</span><span class="sxs-lookup"><span data-stu-id="d007d-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![在 IoT 中樞上設定作業監視][2]

> [!NOTE]
> <span data-ttu-id="d007d-125">選取**Verbose**監視 hello**連線**類別目錄會造成 IoT 中樞 toogenerate 額外的診斷訊息。</span><span class="sxs-lookup"><span data-stu-id="d007d-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="d007d-126">對於所有其他分類，hello **Verbose** hello 數量資訊 IoT 中樞設定變更包含在每個錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d007d-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="d007d-127">事件類別目錄以及 toouse 它們</span><span class="sxs-lookup"><span data-stu-id="d007d-127">Event categories and how toouse them</span></span>

<span data-ttu-id="d007d-128">每個作業監視類別會各自追蹤與 IoT 中樞所進行的不同類型的互動，而每一個監視類別都有結構描述來定義該類別的事件要如何構成。</span><span class="sxs-lookup"><span data-stu-id="d007d-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="d007d-129">裝置身分識別作業</span><span class="sxs-lookup"><span data-stu-id="d007d-129">Device identity operations</span></span>

<span data-ttu-id="d007d-130">hello 裝置識別作業類別目錄會追蹤您嘗試 toocreate 時，發生錯誤、 更新或刪除您的 IoT 中樞身分識別登錄中的項目。</span><span class="sxs-lookup"><span data-stu-id="d007d-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="d007d-131">佈建案例就很適合追蹤此類別。</span><span class="sxs-lookup"><span data-stu-id="d007d-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="d007d-132">裝置遙測</span><span class="sxs-lookup"><span data-stu-id="d007d-132">Device telemetry</span></span>

<span data-ttu-id="d007d-133">hello 裝置遙測類別會追蹤錯誤發生在 hello IoT 中樞，而且相關的 toohello 遙測管線。</span><span class="sxs-lookup"><span data-stu-id="d007d-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="d007d-134">此類別包括在傳送遙測事件 (例如節流) 和接收遙測事件 (例如未經授權的讀取器) 時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="d007d-135">此類別無法攔截 hello 裝置本身上執行的程式碼所造成的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="d007d-136">雲端到裝置的命令</span><span class="sxs-lookup"><span data-stu-id="d007d-136">Cloud-to-device commands</span></span>

<span data-ttu-id="d007d-137">hello 雲端到裝置命令類別會追蹤錯誤發生在 hello IoT 中樞，而且相關的 toohello 雲端到裝置訊息管線。</span><span class="sxs-lookup"><span data-stu-id="d007d-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="d007d-138">這個類別包括在傳送雲端到裝置訊息 (例如未經授權的寄件者)、接收雲端到裝置訊息 (例如超過傳遞計數) 和接收雲端到裝置訊息意見反應 (例如意見反應已過期) 時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="d007d-139">此類別不會攔截錯誤處理的雲端到裝置訊息如果 hello 雲端到裝置訊息已成功傳遞的裝置中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="d007d-140">連線</span><span class="sxs-lookup"><span data-stu-id="d007d-140">Connections</span></span>

<span data-ttu-id="d007d-141">hello 連接類別目錄會追蹤裝置連線，或從 IoT 中樞中斷連線時，發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="d007d-142">若想識別未經授權的連線嘗試，以及在連線品質不佳之區域內的裝置中斷連線時進行追蹤，就很適合追蹤此類別。</span><span class="sxs-lookup"><span data-stu-id="d007d-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="d007d-143">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="d007d-143">File uploads</span></span>

<span data-ttu-id="d007d-144">hello 檔案上傳類別會追蹤錯誤發生在 hello IoT 中樞，而且相關的 toofile 上傳功能。</span><span class="sxs-lookup"><span data-stu-id="d007d-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="d007d-145">此類別包括︰</span><span class="sxs-lookup"><span data-stu-id="d007d-145">This category includes:</span></span>

* <span data-ttu-id="d007d-146">以 hello SAS URI，例如過期之前裝置通知 hello 中樞的已完成上傳時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="d007d-147">無法上傳 hello 裝置所報告。</span><span class="sxs-lookup"><span data-stu-id="d007d-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="d007d-148">IoT 中樞通知訊息建立期間在儲存體中找不到檔案時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="d007d-149">此類別無法攔截 hello 裝置上傳檔案 toostorage，直接時發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="d007d-150">訊息路由</span><span class="sxs-lookup"><span data-stu-id="d007d-150">Message routing</span></span>

<span data-ttu-id="d007d-151">hello 訊息路由類別會追蹤訊息路由評估與端點健全狀況觀察得到的 IoT 中樞期間發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="d007d-152">此類別包含事件，例如當規則評估太"未定義 」，當 IoT 中樞將標示端點為寄不出，並收到來自端點的其他錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="d007d-153">此類別不包含有關 hello 訊息本身 （例如裝置節流錯誤），報告 hello 「 裝置遙測 」 類別下的特定錯誤。</span><span class="sxs-lookup"><span data-stu-id="d007d-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="d007d-154">檢視事件</span><span class="sxs-lookup"><span data-stu-id="d007d-154">View events</span></span>

<span data-ttu-id="d007d-155">您可以使用 hello *iot 中樞總管*工具 tooquickly 測試您的 IoT 中樞產生監視的事件。</span><span class="sxs-lookup"><span data-stu-id="d007d-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="d007d-156">tooinstall hello 工具，請參閱 hello hello 指示[iot 中樞總管][ lnk-iothub-explorer] GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d007d-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="d007d-157">請確定 hello**連線**監視類別設定太**Verbose** hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d007d-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="d007d-158">在命令提示字元中執行 hello 監視端點中的下列命令 tooread hello:</span><span class="sxs-lookup"><span data-stu-id="d007d-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="d007d-159">在另一個命令提示字元，執行下列命令 toosimulate hello 傳送裝置到雲端訊息的裝置：</span><span class="sxs-lookup"><span data-stu-id="d007d-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="d007d-160">hello 第一個命令提示字元會顯示 hello 監視事件 hello 模擬的裝置連線 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d007d-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="d007d-161">連接 toohello 監視端點</span><span class="sxs-lookup"><span data-stu-id="d007d-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="d007d-162">hello 監視上 IoT 中樞端點是事件中樞相容端點。</span><span class="sxs-lookup"><span data-stu-id="d007d-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="d007d-163">您可以使用任何機制可搭配事件中心 tooread 監視郵件從這個端點。</span><span class="sxs-lookup"><span data-stu-id="d007d-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="d007d-164">hello 下列範例會建立基本的讀取器不是適用於高輸送量部署。</span><span class="sxs-lookup"><span data-stu-id="d007d-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="d007d-165">如需如何 tooprocess 訊息從事件中心的詳細資訊，請參閱 hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="d007d-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="d007d-166">tooconnect toohello 監視端點，您需要的連接字串和 hello 端點的名稱。</span><span class="sxs-lookup"><span data-stu-id="d007d-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="d007d-167">hello 步驟會告訴您如何 toofind hello hello 入口網站中的必要值：</span><span class="sxs-lookup"><span data-stu-id="d007d-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="d007d-168">在 [hello 入口網站中，瀏覽 tooyour IoT 中樞資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d007d-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="d007d-169">選擇**作業監視**，並記下的 hello**事件中樞相容名稱**和**事件中樞相容端點**值：</span><span class="sxs-lookup"><span data-stu-id="d007d-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![事件中樞相容端點值][img-endpoints]

1. <span data-ttu-id="d007d-171">選擇 [共用存取原則]，然後選擇 [服務]。</span><span class="sxs-lookup"><span data-stu-id="d007d-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="d007d-172">請記下 hello**主索引鍵**值：</span><span class="sxs-lookup"><span data-stu-id="d007d-172">Make a note of hello **Primary key** value:</span></span>

    ![服務共用存取原則主要金鑰][img-service-key]

<span data-ttu-id="d007d-174">hello 下列 C# 程式碼範例取自 Visual Studio**的傳統 Windows 桌面**C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d007d-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="d007d-175">hello 專案具有 hello **WindowsAzure.ServiceBus**安裝的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="d007d-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="d007d-176">Hello 連接字串預留位置取代為連接字串使用 hello**事件中樞相容端點**和服務**主索引鍵**記下 hello 下列所示的先前值範例：</span><span class="sxs-lookup"><span data-stu-id="d007d-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="d007d-177">取代 hello 監視端點名稱預留位置 hello**事件中樞相容名稱**先前所述的值。</span><span class="sxs-lookup"><span data-stu-id="d007d-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="d007d-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d007d-178">Next steps</span></span>
<span data-ttu-id="d007d-179">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="d007d-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d007d-180">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d007d-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d007d-181">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d007d-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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