---
title: "aaaUnderstand Azure IoT 中樞檔案上傳 |Microsoft 文件"
description: "開發人員指南-使用 IoT 中樞 toomanage 將自裝置 tooan Azure 儲存體 blob 容器的檔案上傳的 hello 檔案上傳功能。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="5a635-103">透過 IoT 中樞上傳檔案</span><span class="sxs-lookup"><span data-stu-id="5a635-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="5a635-104">Hello 中所詳述[IoT 中樞端點][ lnk-endpoints]發行項，裝置可以啟動檔案上傳所傳送的通知，透過面對裝置的端點 (**/devices/ {deviceId} / 檔案**).</span><span class="sxs-lookup"><span data-stu-id="5a635-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="5a635-105">IoT 中樞時裝置通知 IoT 中樞時上, 傳已完成，會傳送檔案上傳通知訊息透過 hello **/messages/servicebound/filenotifications**面對服務的端點。</span><span class="sxs-lookup"><span data-stu-id="5a635-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="5a635-106">而不是仲介訊息透過本身的 IoT 中樞，IoT 中樞而是做為發送器 tooan 相關聯的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a635-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="5a635-107">裝置會要求在特定 toohello 檔案 hello 裝置 IoT 中樞中的儲存體語彙基元希望 tooupload。</span><span class="sxs-lookup"><span data-stu-id="5a635-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="5a635-108">hello 裝置會使用 SAS URI tooupload hello 檔案 toostorage hello 和 hello 裝置 hello 上傳完成時傳送完成 tooIoT 中樞的通知。</span><span class="sxs-lookup"><span data-stu-id="5a635-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="5a635-109">IoT 中樞檢查 hello 檔案上傳已完成，並將檔案上傳通知訊息 toohello 服務向檔案通知端點。</span><span class="sxs-lookup"><span data-stu-id="5a635-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="5a635-110">您上傳的檔案 tooIoT 中樞，從裝置之前，您必須設定您的中樞[關聯的 Azure 儲存體][ lnk-associate-storage]帳戶 tooit。</span><span class="sxs-lookup"><span data-stu-id="5a635-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="5a635-111">您的裝置可以接著[初始化上傳][ lnk-initialize]然後[通知 IoT 中樞][ lnk-notify] hello 上傳完成時。</span><span class="sxs-lookup"><span data-stu-id="5a635-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="5a635-112">（選擇性） 當裝置通知 IoT 中樞 hello 傳已完成，可以產生 hello 服務[通知訊息][lnk-service-notification]。</span><span class="sxs-lookup"><span data-stu-id="5a635-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="5a635-113">當 toouse</span><span class="sxs-lookup"><span data-stu-id="5a635-113">When toouse</span></span>

<span data-ttu-id="5a635-114">使用檔案上傳 toosend 媒體檔案或間斷連接的裝置或壓縮的 toosave 頻寬所上傳大型遙測批次。</span><span class="sxs-lookup"><span data-stu-id="5a635-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="5a635-115">參照太[裝置到雲端通訊指引][ lnk-d2c-guidance]如果不確定之間使用報告的內容、 裝置到雲端訊息或檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="5a635-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="5a635-116">讓 Azure 儲存體帳戶與 IoT 中樞產生關聯</span><span class="sxs-lookup"><span data-stu-id="5a635-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="5a635-117">toouse hello 檔案上傳功能，您必須先連結的 Azure 儲存體帳戶 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5a635-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="5a635-118">您可以透過 hello 完成這項工作[Azure 入口網站][lnk-management-portal]，或以程式設計方式透過 hello [IoT 中樞資源提供者 REST Api] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="5a635-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="5a635-119">一旦您將建立 Azure 儲存體帳戶關聯與 IoT 中樞，hello 服務會傳回 SAS URI tooa 裝置 hello 裝置啟動檔案上傳要求。</span><span class="sxs-lookup"><span data-stu-id="5a635-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="5a635-120">hello [Azure IoT Sdk] [ lnk-sdks]自動控制代碼擷取 hello SAS URI 上, 傳 hello 檔案，並通知已完成上傳的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5a635-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="5a635-121">初始化檔案上傳</span><span class="sxs-lookup"><span data-stu-id="5a635-121">Initialize a file upload</span></span>
<span data-ttu-id="5a635-122">IoT 中心已特別針對裝置 toorequest SAS URI，以進行儲存體 tooupload 檔案端點。</span><span class="sxs-lookup"><span data-stu-id="5a635-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="5a635-123">tooinitiate hello 檔案上傳程序，hello 裝置傳送 POST 要求太`{iot hub}.azure-devices.net/devices/{deviceId}/files`以 hello 下列 JSON 主體：</span><span class="sxs-lookup"><span data-stu-id="5a635-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="5a635-124">IoT 中樞傳回 hello 下列哪一個 hello 裝置使用 tooupload hello 檔案的資料：</span><span class="sxs-lookup"><span data-stu-id="5a635-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="5a635-125">已被取代︰使用 GET 初始化檔案上傳</span><span class="sxs-lookup"><span data-stu-id="5a635-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="5a635-126">本節說明如何針對已被取代的功能 tooreceive 從 IoT 中樞的 SAS URI。</span><span class="sxs-lookup"><span data-stu-id="5a635-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="5a635-127">使用先前所述的 hello POST 方法。</span><span class="sxs-lookup"><span data-stu-id="5a635-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="5a635-128">IoT 中樞有兩個 REST 端點 toosupport 檔案上傳一個 tooget hello SAS URI 進行儲存及 hello 的已完成上傳其他 toonotify hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5a635-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="5a635-129">hello 裝置啟始 hello 檔案上傳程序傳送給在 GET toohello IoT 中樞`{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`。</span><span class="sxs-lookup"><span data-stu-id="5a635-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="5a635-130">hello IoT 中樞傳回：</span><span class="sxs-lookup"><span data-stu-id="5a635-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="5a635-131">上傳特定 toohello 檔案 toobe SAS URI。</span><span class="sxs-lookup"><span data-stu-id="5a635-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="5a635-132">相互關聯識別碼 toobe，hello 上傳完成後使用。</span><span class="sxs-lookup"><span data-stu-id="5a635-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="5a635-133">通知 IoT 中樞已完成檔案上傳</span><span class="sxs-lookup"><span data-stu-id="5a635-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="5a635-134">裝置 hello 負責上傳 hello 檔案 toostorage 使用 hello Azure 儲存體 Sdk。</span><span class="sxs-lookup"><span data-stu-id="5a635-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="5a635-135">Hello 上傳完成時，hello 裝置傳送 POST 要求太`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications`以 hello 下列 JSON 主體：</span><span class="sxs-lookup"><span data-stu-id="5a635-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="5a635-136">hello 值`isSuccess`是布林值表示是否已成功上傳 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="5a635-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="5a635-137">hello 狀態碼`statusCode`是 hello hello hello 檔案 toostorage 上, 傳的狀態和 hello`statusDescription`對應 toohello `statusCode`。</span><span class="sxs-lookup"><span data-stu-id="5a635-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="5a635-138">參考主題：</span><span class="sxs-lookup"><span data-stu-id="5a635-138">Reference topics:</span></span>

<span data-ttu-id="5a635-139">hello 下列參考主題提供您有關上傳檔案，從裝置的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5a635-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="5a635-140">檔案上傳通知</span><span class="sxs-lookup"><span data-stu-id="5a635-140">File upload notifications</span></span>

<span data-ttu-id="5a635-141">（選擇性） 當裝置通知 IoT 中樞時，已完成上傳，IoT 中樞可以產生通知訊息包含 hello hello 檔案的名稱和儲存位置。</span><span class="sxs-lookup"><span data-stu-id="5a635-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="5a635-142">如[端點][lnk-endpoints]中所述，IoT 中樞會透過面向服務的端點 (**/messages/servicebound/fileuploadnotifications**) 利用訊息來傳遞檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="5a635-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="5a635-143">hello 接收語意，檔案上傳通知為相同 hello 與雲端到裝置訊息和 hello 相同[訊息生命週期][lnk-lifecycle]。</span><span class="sxs-lookup"><span data-stu-id="5a635-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="5a635-144">每個擷取自 hello 檔案上傳通知端點的訊息是 JSON 記錄以 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="5a635-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="5a635-145">屬性</span><span class="sxs-lookup"><span data-stu-id="5a635-145">Property</span></span> | <span data-ttu-id="5a635-146">說明</span><span class="sxs-lookup"><span data-stu-id="5a635-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a635-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="5a635-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="5a635-148">建立 hello 通知時，指出時間戳記。</span><span class="sxs-lookup"><span data-stu-id="5a635-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="5a635-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="5a635-149">DeviceId</span></span> |<span data-ttu-id="5a635-150">**DeviceId** hello 裝置 hello 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="5a635-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="5a635-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="5a635-151">BlobUri</span></span> |<span data-ttu-id="5a635-152">Hello 上傳檔案的 URI。</span><span class="sxs-lookup"><span data-stu-id="5a635-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="5a635-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="5a635-153">BlobName</span></span> |<span data-ttu-id="5a635-154">Hello 名稱上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="5a635-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="5a635-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="5a635-155">LastUpdatedTime</span></span> |<span data-ttu-id="5a635-156">指出 hello 檔案上次更新時間戳記。</span><span class="sxs-lookup"><span data-stu-id="5a635-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="5a635-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="5a635-157">BlobSizeInBytes</span></span> |<span data-ttu-id="5a635-158">Hello 大小上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="5a635-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="5a635-159">**範例**。</span><span class="sxs-lookup"><span data-stu-id="5a635-159">**Example**.</span></span> <span data-ttu-id="5a635-160">此範例會顯示 hello 內文的檔案上傳通知訊息。</span><span class="sxs-lookup"><span data-stu-id="5a635-160">This example shows hello body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="5a635-161">檔案上傳通知組態選項</span><span class="sxs-lookup"><span data-stu-id="5a635-161">File upload notification configuration options</span></span>

<span data-ttu-id="5a635-162">每個 IoT 中樞會公開下列檔案上傳通知組態選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a635-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="5a635-163">屬性</span><span class="sxs-lookup"><span data-stu-id="5a635-163">Property</span></span> | <span data-ttu-id="5a635-164">說明</span><span class="sxs-lookup"><span data-stu-id="5a635-164">Description</span></span> | <span data-ttu-id="5a635-165">範圍和預設值</span><span class="sxs-lookup"><span data-stu-id="5a635-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a635-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="5a635-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="5a635-167">控制是否檔案上傳通知會寫入 toohello 檔案通知端點。</span><span class="sxs-lookup"><span data-stu-id="5a635-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="5a635-168">布林</span><span class="sxs-lookup"><span data-stu-id="5a635-168">Bool.</span></span> <span data-ttu-id="5a635-169">預設值：True。</span><span class="sxs-lookup"><span data-stu-id="5a635-169">Default: True.</span></span> |
| <span data-ttu-id="5a635-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="5a635-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="5a635-171">檔案上傳通知的預設 TTL。</span><span class="sxs-lookup"><span data-stu-id="5a635-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="5a635-172">向上 too48H ISO_8601 間隔 （最小的 1 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="5a635-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="5a635-173">預設值︰1 小時。</span><span class="sxs-lookup"><span data-stu-id="5a635-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="5a635-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="5a635-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="5a635-175">Hello 檔案上傳通知佇列的鎖定持續時間。</span><span class="sxs-lookup"><span data-stu-id="5a635-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="5a635-176">5 too300 秒 （最小值 5 秒）。</span><span class="sxs-lookup"><span data-stu-id="5a635-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="5a635-177">預設值：60 秒。</span><span class="sxs-lookup"><span data-stu-id="5a635-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="5a635-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="5a635-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="5a635-179">最大傳遞計數 hello 檔案上傳通知佇列。</span><span class="sxs-lookup"><span data-stu-id="5a635-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="5a635-180">1 too100。</span><span class="sxs-lookup"><span data-stu-id="5a635-180">1 too100.</span></span> <span data-ttu-id="5a635-181">預設值 = 100。</span><span class="sxs-lookup"><span data-stu-id="5a635-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="5a635-182">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="5a635-182">Additional reference material</span></span>

<span data-ttu-id="5a635-183">Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：</span><span class="sxs-lookup"><span data-stu-id="5a635-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="5a635-184">[IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。</span><span class="sxs-lookup"><span data-stu-id="5a635-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="5a635-185">[節流和配額][ lnk-quotas]描述 hello 配額和節流套用 toohello IoT 中心服務的行為。</span><span class="sxs-lookup"><span data-stu-id="5a635-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="5a635-186">[Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用的 Sdk。</span><span class="sxs-lookup"><span data-stu-id="5a635-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="5a635-187">[IoT 中樞的查詢語言][ lnk-query]描述 hello 查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5a635-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="5a635-188">[IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5a635-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a635-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a635-189">Next steps</span></span>

<span data-ttu-id="5a635-190">現在您已經學會如何 tooupload 檔案從使用 IoT 中樞的裝置，您可能想要遵循 IoT 中樞開發人員指南主題 hello:</span><span class="sxs-lookup"><span data-stu-id="5a635-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="5a635-191">[在 IoT 中樞管理裝置身分識別][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="5a635-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="5a635-192">[控制存取 tooIoT 中樞][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="5a635-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="5a635-193">[使用裝置雙 toosynchronize 狀態和組態][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="5a635-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="5a635-194">[在裝置上叫用直接方法][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="5a635-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="5a635-195">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="5a635-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="5a635-196">如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程中的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a635-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="5a635-197">[從裝置 toohello tooupload 檔案定域機組與 IoT 中樞][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="5a635-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
