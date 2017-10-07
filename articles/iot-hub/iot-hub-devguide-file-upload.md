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
# <a name="upload-files-with-iot-hub"></a>透過 IoT 中樞上傳檔案

Hello 中所詳述[IoT 中樞端點][ lnk-endpoints]發行項，裝置可以啟動檔案上傳所傳送的通知，透過面對裝置的端點 (**/devices/ {deviceId} / 檔案**). IoT 中樞時裝置通知 IoT 中樞時上, 傳已完成，會傳送檔案上傳通知訊息透過 hello **/messages/servicebound/filenotifications**面對服務的端點。

而不是仲介訊息透過本身的 IoT 中樞，IoT 中樞而是做為發送器 tooan 相關聯的 Azure 儲存體帳戶。 裝置會要求在特定 toohello 檔案 hello 裝置 IoT 中樞中的儲存體語彙基元希望 tooupload。 hello 裝置會使用 SAS URI tooupload hello 檔案 toostorage hello 和 hello 裝置 hello 上傳完成時傳送完成 tooIoT 中樞的通知。 IoT 中樞檢查 hello 檔案上傳已完成，並將檔案上傳通知訊息 toohello 服務向檔案通知端點。

您上傳的檔案 tooIoT 中樞，從裝置之前，您必須設定您的中樞[關聯的 Azure 儲存體][ lnk-associate-storage]帳戶 tooit。

您的裝置可以接著[初始化上傳][ lnk-initialize]然後[通知 IoT 中樞][ lnk-notify] hello 上傳完成時。 （選擇性） 當裝置通知 IoT 中樞 hello 傳已完成，可以產生 hello 服務[通知訊息][lnk-service-notification]。

### <a name="when-toouse"></a>當 toouse

使用檔案上傳 toosend 媒體檔案或間斷連接的裝置或壓縮的 toosave 頻寬所上傳大型遙測批次。

參照太[裝置到雲端通訊指引][ lnk-d2c-guidance]如果不確定之間使用報告的內容、 裝置到雲端訊息或檔案上傳。

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>讓 Azure 儲存體帳戶與 IoT 中樞產生關聯

toouse hello 檔案上傳功能，您必須先連結的 Azure 儲存體帳戶 toohello IoT 中樞。 您可以透過 hello 完成這項工作[Azure 入口網站][lnk-management-portal]，或以程式設計方式透過 hello [IoT 中樞資源提供者 REST Api] [ lnk-resource-provider-apis]. 一旦您將建立 Azure 儲存體帳戶關聯與 IoT 中樞，hello 服務會傳回 SAS URI tooa 裝置 hello 裝置啟動檔案上傳要求。

> [!NOTE]
> hello [Azure IoT Sdk] [ lnk-sdks]自動控制代碼擷取 hello SAS URI 上, 傳 hello 檔案，並通知已完成上傳的 IoT 中樞。


## <a name="initialize-a-file-upload"></a>初始化檔案上傳
IoT 中心已特別針對裝置 toorequest SAS URI，以進行儲存體 tooupload 檔案端點。 tooinitiate hello 檔案上傳程序，hello 裝置傳送 POST 要求太`{iot hub}.azure-devices.net/devices/{deviceId}/files`以 hello 下列 JSON 主體：

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

IoT 中樞傳回 hello 下列哪一個 hello 裝置使用 tooupload hello 檔案的資料：

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>已被取代︰使用 GET 初始化檔案上傳

> [!NOTE]
> 本節說明如何針對已被取代的功能 tooreceive 從 IoT 中樞的 SAS URI。 使用先前所述的 hello POST 方法。

IoT 中樞有兩個 REST 端點 toosupport 檔案上傳一個 tooget hello SAS URI 進行儲存及 hello 的已完成上傳其他 toonotify hello IoT 中樞。 hello 裝置啟始 hello 檔案上傳程序傳送給在 GET toohello IoT 中樞`{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`。 hello IoT 中樞傳回：

* 上傳特定 toohello 檔案 toobe SAS URI。
* 相互關聯識別碼 toobe，hello 上傳完成後使用。

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>通知 IoT 中樞已完成檔案上傳

裝置 hello 負責上傳 hello 檔案 toostorage 使用 hello Azure 儲存體 Sdk。 Hello 上傳完成時，hello 裝置傳送 POST 要求太`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications`以 hello 下列 JSON 主體：

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

hello 值`isSuccess`是布林值表示是否已成功上傳 hello 檔案。 hello 狀態碼`statusCode`是 hello hello hello 檔案 toostorage 上, 傳的狀態和 hello`statusDescription`對應 toohello `statusCode`。

## <a name="reference-topics"></a>參考主題：

hello 下列參考主題提供您有關上傳檔案，從裝置的詳細資訊。

## <a name="file-upload-notifications"></a>檔案上傳通知

（選擇性） 當裝置通知 IoT 中樞時，已完成上傳，IoT 中樞可以產生通知訊息包含 hello hello 檔案的名稱和儲存位置。

如[端點][lnk-endpoints]中所述，IoT 中樞會透過面向服務的端點 (**/messages/servicebound/fileuploadnotifications**) 利用訊息來傳遞檔案上傳通知。 hello 接收語意，檔案上傳通知為相同 hello 與雲端到裝置訊息和 hello 相同[訊息生命週期][lnk-lifecycle]。 每個擷取自 hello 檔案上傳通知端點的訊息是 JSON 記錄以 hello 下列屬性：

| 屬性 | 說明 |
| --- | --- |
| EnqueuedTimeUtc |建立 hello 通知時，指出時間戳記。 |
| deviceId |**DeviceId** hello 裝置 hello 檔案上傳。 |
| BlobUri |Hello 上傳檔案的 URI。 |
| BlobName |Hello 名稱上傳檔案。 |
| LastUpdatedTime |指出 hello 檔案上次更新時間戳記。 |
| BlobSizeInBytes |Hello 大小上傳檔案。 |

**範例**。 此範例會顯示 hello 內文的檔案上傳通知訊息。

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

## <a name="file-upload-notification-configuration-options"></a>檔案上傳通知組態選項

每個 IoT 中樞會公開下列檔案上傳通知組態選項的 hello:

| 屬性 | 說明 | 範圍和預設值 |
| --- | --- | --- |
| **enableFileUploadNotifications** |控制是否檔案上傳通知會寫入 toohello 檔案通知端點。 |布林 預設值：True。 |
| **fileNotifications.ttlAsIso8601** |檔案上傳通知的預設 TTL。 |向上 too48H ISO_8601 間隔 （最小的 1 分鐘）。 預設值︰1 小時。 |
| **fileNotifications.lockDuration** |Hello 檔案上傳通知佇列的鎖定持續時間。 |5 too300 秒 （最小值 5 秒）。 預設值：60 秒。 |
| **fileNotifications.maxDeliveryCount** |最大傳遞計數 hello 檔案上傳通知佇列。 |1 too100。 預設值 = 100。 |

## <a name="additional-reference-material"></a>其他參考資料

Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：

* [IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。
* [節流和配額][ lnk-quotas]描述 hello 配額和節流套用 toohello IoT 中心服務的行為。
* [Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用的 Sdk。
* [IoT 中樞的查詢語言][ lnk-query]描述 hello 查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。
* [IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。

## <a name="next-steps"></a>後續步驟

現在您已經學會如何 tooupload 檔案從使用 IoT 中樞的裝置，您可能想要遵循 IoT 中樞開發人員指南主題 hello:

* [在 IoT 中樞管理裝置身分識別][lnk-devguide-identities]
* [控制存取 tooIoT 中樞][lnk-devguide-security]
* [使用裝置雙 toosynchronize 狀態和組態][lnk-devguide-device-twins]
* [在裝置上叫用直接方法][lnk-devguide-directmethods]
* [排程多個裝置上的作業][lnk-devguide-jobs]

如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程中的 hello:

* [從裝置 toohello tooupload 檔案定域機組與 IoT 中樞][lnk-fileupload-tutorial]

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
