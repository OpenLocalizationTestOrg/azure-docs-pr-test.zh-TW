---
title: "了解 Azure IoT 中樞檔案上傳 | Microsoft Docs"
description: "開發人員指南 - 使用 IoT 中樞的檔案上傳功能，管理將檔案從裝置上傳至 Azure 儲存體 blob 容器。"
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
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="9269c-103">透過 IoT 中樞上傳檔案</span><span class="sxs-lookup"><span data-stu-id="9269c-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="9269c-104">如 [IoT 中樞端點][lnk-endpoints]一文所詳述，裝置可以藉由透過面向裝置的端點 (**/devices/{deviceId}/files**) 傳送通知，來起始檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="9269c-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="9269c-105">當裝置向 IoT 中樞告知上傳作業完成時，IoT 中樞會透過 **/messages/servicebound/filenotifications** 面向服務的端點傳送檔案上傳通知訊息。</span><span class="sxs-lookup"><span data-stu-id="9269c-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="9269c-106">不是透過 IoT 中樞本身的代理訊息，IoT 中樞會做為相關聯 Azure 儲存體帳戶的發送器。</span><span class="sxs-lookup"><span data-stu-id="9269c-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="9269c-107">裝置會向 IoT 中樞要求儲存體權杖，這是裝置想要上傳的檔案的特定權杖。</span><span class="sxs-lookup"><span data-stu-id="9269c-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="9269c-108">裝置會使用 SAS URI，將檔案上傳至儲存體，上傳完成時，裝置會將完成的通知傳送到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9269c-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="9269c-109">IoT 中樞會在確認檔案上傳已完成後，再將檔案上傳通知訊息新增至服務面向檔案通知端點。</span><span class="sxs-lookup"><span data-stu-id="9269c-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="9269c-110">將檔案從裝置上傳到 IoT 中樞之前，您必須先對中樞[關聯 Azure 儲存體][lnk-associate-storage]帳戶以設定中樞。</span><span class="sxs-lookup"><span data-stu-id="9269c-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="9269c-111">接著，您的裝置就可以[初始化上傳][lnk-initialize]，然後在上傳完成時[通知 IoT 中樞][lnk-notify]。</span><span class="sxs-lookup"><span data-stu-id="9269c-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="9269c-112">(選擇性) 當裝置將上傳已完成的狀態通知 IoT 中樞時，服務就會產生[通知訊息][lnk-service-notification]。</span><span class="sxs-lookup"><span data-stu-id="9269c-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="9269c-113">使用時機</span><span class="sxs-lookup"><span data-stu-id="9269c-113">When to use</span></span>

<span data-ttu-id="9269c-114">使用檔案上傳來傳送間歇性連線裝置所上傳或為了節省頻寬而壓縮的媒體檔案和大型遙測批次。</span><span class="sxs-lookup"><span data-stu-id="9269c-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="9269c-115">如果不確定要使用報告屬性、裝置對雲端訊息或檔案上傳，請參閱[裝置到雲端通訊指引][lnk-d2c-guidance]。</span><span class="sxs-lookup"><span data-stu-id="9269c-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="9269c-116">讓 Azure 儲存體帳戶與 IoT 中樞產生關聯</span><span class="sxs-lookup"><span data-stu-id="9269c-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="9269c-117">若要使用檔案上傳功能，您必須先將 Azure 儲存體帳戶連結至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9269c-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="9269c-118">您可以透過 [Azure 入口網站][lnk-management-portal]完成此工作，或透過 [IoT 中樞資源提供者 REST API][lnk-resource-provider-apis] 以程式設計方式完成此工作。</span><span class="sxs-lookup"><span data-stu-id="9269c-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="9269c-119">一旦您將 Azure 儲存體帳戶與 IoT 中樞產生關聯，服務會在裝置起始檔案上傳要求時，將 SAS URI 傳回至裝置。</span><span class="sxs-lookup"><span data-stu-id="9269c-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="9269c-120">[Azure IoT SDK][lnk-sdks] 會自動處理擷取 SAS URI、上傳檔案，並且通知 IoT 中樞已完成上傳。</span><span class="sxs-lookup"><span data-stu-id="9269c-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="9269c-121">初始化檔案上傳</span><span class="sxs-lookup"><span data-stu-id="9269c-121">Initialize a file upload</span></span>
<span data-ttu-id="9269c-122">IoT 中樞擁有專供裝置用來要求儲存體 SAS URI 以便上傳檔案的端點。</span><span class="sxs-lookup"><span data-stu-id="9269c-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="9269c-123">為了起始檔案上傳程序，裝置會將含有下列 JSON 主體的 POST 要求傳送到 `{iot hub}.azure-devices.net/devices/{deviceId}/files`：</span><span class="sxs-lookup"><span data-stu-id="9269c-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="9269c-124">「IoT 中樞」會傳回下列資料，供裝置用來上傳檔案︰</span><span class="sxs-lookup"><span data-stu-id="9269c-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="9269c-125">已被取代︰使用 GET 初始化檔案上傳</span><span class="sxs-lookup"><span data-stu-id="9269c-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="9269c-126">本節說明如何從 IoT 中樞接收 SAS URI 的功能，但此功能已被取代。</span><span class="sxs-lookup"><span data-stu-id="9269c-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="9269c-127">請使用先前所述的 POST 方法。</span><span class="sxs-lookup"><span data-stu-id="9269c-127">Use the POST method described previously.</span></span>

<span data-ttu-id="9269c-128">IoT 中樞有兩個 REST 端點可以支援檔案上傳，一個用來取得儲存體的 SAS URI，另一個用來通知 IoT 中樞已完成上傳。</span><span class="sxs-lookup"><span data-stu-id="9269c-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="9269c-129">裝置會起始檔案上傳程序，方法是將 GET 傳送至 IoT 中樞的 `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`。</span><span class="sxs-lookup"><span data-stu-id="9269c-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="9269c-130">IoT 中樞會傳回：</span><span class="sxs-lookup"><span data-stu-id="9269c-130">The IoT hub returns:</span></span>

* <span data-ttu-id="9269c-131">要上傳之檔案專屬的 SAS URI。</span><span class="sxs-lookup"><span data-stu-id="9269c-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="9269c-132">要在上傳完成後使用的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="9269c-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="9269c-133">通知 IoT 中樞已完成檔案上傳</span><span class="sxs-lookup"><span data-stu-id="9269c-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="9269c-134">裝置會負責使用 Azure 儲存體 SDK 將檔案上傳至儲存體。</span><span class="sxs-lookup"><span data-stu-id="9269c-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="9269c-135">上傳完成時，裝置會將具有下列 JSON 主體的 POST 要求傳送至 `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications`︰</span><span class="sxs-lookup"><span data-stu-id="9269c-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="9269c-136">`isSuccess` 的值是一個代表是否已成功上傳檔案的布林值。</span><span class="sxs-lookup"><span data-stu-id="9269c-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="9269c-137">`statusCode` 的狀態碼是檔案上傳至儲存體的狀態，而且 `statusDescription` 會對應至 `statusCode`。</span><span class="sxs-lookup"><span data-stu-id="9269c-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="9269c-138">參考主題：</span><span class="sxs-lookup"><span data-stu-id="9269c-138">Reference topics:</span></span>

<span data-ttu-id="9269c-139">下列參考主題會提供您關於從裝置上傳檔案的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9269c-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="9269c-140">檔案上傳通知</span><span class="sxs-lookup"><span data-stu-id="9269c-140">File upload notifications</span></span>

<span data-ttu-id="9269c-141">(選擇性) 當裝置向 IoT 中樞告知上傳已完成時，IoT 中樞會產生通知訊息，其中包含檔案的名稱和儲存位置。</span><span class="sxs-lookup"><span data-stu-id="9269c-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="9269c-142">如[端點][lnk-endpoints]中所述，IoT 中樞會透過面向服務的端點 (**/messages/servicebound/fileuploadnotifications**) 利用訊息來傳遞檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="9269c-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="9269c-143">檔案上傳通知的接收語意與雲端到裝置訊息的接收語意相同，並且具有相同的[訊息生命週期][lnk-lifecycle]。</span><span class="sxs-lookup"><span data-stu-id="9269c-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="9269c-144">從檔案上傳通知端點擷取的每則訊息是具有下列屬性的 JSON 記錄：</span><span class="sxs-lookup"><span data-stu-id="9269c-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="9269c-145">屬性</span><span class="sxs-lookup"><span data-stu-id="9269c-145">Property</span></span> | <span data-ttu-id="9269c-146">說明</span><span class="sxs-lookup"><span data-stu-id="9269c-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9269c-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="9269c-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="9269c-148">指出通知建立時間的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="9269c-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="9269c-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="9269c-149">DeviceId</span></span> |<span data-ttu-id="9269c-150">**DeviceId** 。</span><span class="sxs-lookup"><span data-stu-id="9269c-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="9269c-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="9269c-151">BlobUri</span></span> |<span data-ttu-id="9269c-152">上傳檔案的 URI。</span><span class="sxs-lookup"><span data-stu-id="9269c-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="9269c-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="9269c-153">BlobName</span></span> |<span data-ttu-id="9269c-154">上傳檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="9269c-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="9269c-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="9269c-155">LastUpdatedTime</span></span> |<span data-ttu-id="9269c-156">指出上次更新檔案的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="9269c-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="9269c-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="9269c-157">BlobSizeInBytes</span></span> |<span data-ttu-id="9269c-158">上傳檔案的大小。</span><span class="sxs-lookup"><span data-stu-id="9269c-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="9269c-159">**範例**。</span><span class="sxs-lookup"><span data-stu-id="9269c-159">**Example**.</span></span> <span data-ttu-id="9269c-160">此範例顯示檔案上傳通知訊息的本文。</span><span class="sxs-lookup"><span data-stu-id="9269c-160">This example shows the body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="9269c-161">檔案上傳通知組態選項</span><span class="sxs-lookup"><span data-stu-id="9269c-161">File upload notification configuration options</span></span>

<span data-ttu-id="9269c-162">每個 IoT 中樞都會針對檔案上傳通知公開下列組態選項：</span><span class="sxs-lookup"><span data-stu-id="9269c-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="9269c-163">屬性</span><span class="sxs-lookup"><span data-stu-id="9269c-163">Property</span></span> | <span data-ttu-id="9269c-164">說明</span><span class="sxs-lookup"><span data-stu-id="9269c-164">Description</span></span> | <span data-ttu-id="9269c-165">範圍和預設值</span><span class="sxs-lookup"><span data-stu-id="9269c-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9269c-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="9269c-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="9269c-167">控制是否將檔案上傳通知寫入檔案通知端點。</span><span class="sxs-lookup"><span data-stu-id="9269c-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="9269c-168">布林</span><span class="sxs-lookup"><span data-stu-id="9269c-168">Bool.</span></span> <span data-ttu-id="9269c-169">預設值：True。</span><span class="sxs-lookup"><span data-stu-id="9269c-169">Default: True.</span></span> |
| <span data-ttu-id="9269c-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="9269c-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="9269c-171">檔案上傳通知的預設 TTL。</span><span class="sxs-lookup"><span data-stu-id="9269c-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="9269c-172">ISO_8601 間隔高達 48H (最小為 1 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="9269c-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="9269c-173">預設值︰1 小時。</span><span class="sxs-lookup"><span data-stu-id="9269c-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="9269c-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="9269c-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="9269c-175">檔案上傳通知佇列的鎖定持續時間。</span><span class="sxs-lookup"><span data-stu-id="9269c-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="9269c-176">5 到 300 秒 (最小值 5 秒)。</span><span class="sxs-lookup"><span data-stu-id="9269c-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="9269c-177">預設值：60 秒。</span><span class="sxs-lookup"><span data-stu-id="9269c-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="9269c-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="9269c-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="9269c-179">檔案上傳通知佇列的傳遞計數上限。</span><span class="sxs-lookup"><span data-stu-id="9269c-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="9269c-180">1 到 100。</span><span class="sxs-lookup"><span data-stu-id="9269c-180">1 to 100.</span></span> <span data-ttu-id="9269c-181">預設值 = 100。</span><span class="sxs-lookup"><span data-stu-id="9269c-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="9269c-182">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="9269c-182">Additional reference material</span></span>

<span data-ttu-id="9269c-183">IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="9269c-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="9269c-184">[IoT 中樞端點][lnk-endpoints]說明每個 IoT 中樞公開給執行階段和管理作業的各種端點。</span><span class="sxs-lookup"><span data-stu-id="9269c-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="9269c-185">[節流和配額][lnk-quotas]描述適用於 IoT 中樞服務的配額和節流行為。</span><span class="sxs-lookup"><span data-stu-id="9269c-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="9269c-186">[Azure IoT 裝置和服務 SDK][lnk-sdks] 列出各種語言 SDK，可供您在開發與「IoT 中樞」互動的裝置和服務應用程式時使用。</span><span class="sxs-lookup"><span data-stu-id="9269c-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="9269c-187">[IoT 中樞查詢語言][lnk-query]描述可用來從 IoT 中樞擷取有關裝置對應項和作業之資訊的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="9269c-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="9269c-188">[IoT 中樞 MQTT 支援][lnk-devguide-mqtt]針對 MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9269c-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9269c-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9269c-189">Next steps</span></span>

<span data-ttu-id="9269c-190">現在您已了解如何使用 IoT 中樞從裝置上傳檔案，接下來您可能對下列 IoT 中樞開發人員指南主題感興趣︰</span><span class="sxs-lookup"><span data-stu-id="9269c-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="9269c-191">[在 IoT 中樞管理裝置身分識別][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="9269c-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="9269c-192">[控制 IoT 中樞的存取權][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="9269c-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="9269c-193">[使用裝置對應項同步處理狀態和組態][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="9269c-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="9269c-194">[在裝置上叫用直接方法][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="9269c-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="9269c-195">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="9269c-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="9269c-196">如果您想要嘗試本文章所述的概念，您可能會對下列 IoT 中樞教學課程感興趣：</span><span class="sxs-lookup"><span data-stu-id="9269c-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="9269c-197">[如何使用 IoT 中樞從裝置將檔案上傳至雲端][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="9269c-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
