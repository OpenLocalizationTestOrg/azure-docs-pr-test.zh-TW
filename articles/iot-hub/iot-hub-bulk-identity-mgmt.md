---
title: "Azure IoT Hub 裝置身分識別的 aaaImport 匯出 |Microsoft 文件"
description: "如何 toouse hello Azure IoT 服務 SDK tooperform 大量作業對 hello 身分識別登錄 tooimport 及匯出裝置身分識別。 匯入作業可讓您 toocreate、 更新和刪除大量的裝置身分識別。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>管理大量的 IoT 中樞裝置身分識別

每個 IoT 中樞有 toocreate 每一裝置的資源可用於 hello 服務身分識別登錄。 hello 身分識別登錄也可讓您 toocontrol 存取 toohello 面對裝置的端點。 本文說明如何 tooimport 及匯出裝置身分識別在大量 tooand 從身分識別登錄。

匯入和匯出作業進行中的 hello 內容*作業*可讓您與 IoT 中樞 tooexecute 大量服務作業。

hello **RegistryManager**類別包含 hello **ExportDevicesAsync**和**ImportDevicesAsync**使用 hello 方法**作業**架構。 這些方法 tooexport，匯入，可讓您，而且同步處理的 IoT 中樞身分識別登錄的 hello 全部內容。

## <a name="what-are-jobs"></a>什麼是作業？

身分識別登錄作業使用 hello**作業**系統當 hello 作業：

* 有可能很長的執行時間會比較 toostandard 執行階段作業。
* 傳回大量的資料 toohello 使用者。

而不是單一 API 呼叫正在等候或封鎖 hello hello 作業結果，hello 作業以非同步方式建立**作業**該 IoT 中樞。 hello 作業然後立即傳回**JobProperties**物件。

hello 下列 C# 程式碼片段示範如何 toocreate 匯出工作：

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> toouse hello **RegistryManager**類別 C# 程式碼中，新增 hello **Microsoft.Azure.Devices** NuGet 封裝 tooyour 專案。 hello **RegistryManager**類別是在 hello **Microsoft.Azure.Devices**命名空間。

您可以使用 hello **RegistryManager**類別 hello tooquery hello 狀態**作業**使用傳回的 hello **JobProperties**中繼資料。

hello 下列 C# 程式碼片段示範如何 toopoll 每五秒 toosee 如果 hello 作業已完成執行：

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a>匯出裝置

使用 hello **ExportDevicesAsync** IoT 中樞身分識別登錄 tooan 方法 tooexport hello 整個[Azure 儲存體](../storage/index.md)blob 容器使用[共用存取簽章](../storage/common/storage-security-guide.md#data-plane-security)。

這個方法可讓您 toocreate 可靠的備份中的 blob 容器，您可以控制您裝置的資訊。

hello **ExportDevicesAsync**方法需要兩個參數：

* 包含 Blob 容器 URI 的「字串」 。 此 URI 必須包含授與寫入權限 toohello 容器的 SAS 權杖。 hello 作業會建立區塊 blob，在此容器 toostore hello 序列化匯出裝置資料中。 hello SAS 權杖必須包含這些權限：

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* A*布林*，指出您是否想 tooexclude 驗證金鑰，從您匯出的資料。 若為 **false**，驗證金鑰就會包含在匯出輸出中。 否則，會將金鑰匯出為 **null**。

hello 下列 C# 程式碼片段示範 tooinitiate 匯出工作，其包含在 hello 的裝置驗證金鑰匯出資料，然後輪詢完成的方式：

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

hello 工作存放其輸出 hello 提供 blob 容器中為 hello 同名的區塊 blob **devices.txt**。 hello 輸出資料會組成每行一個裝置的 JSON 序列化裝置資料。

hello 下列範例顯示 hello 輸出資料：

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

如果裝置有兩個資料，然後 hello 兩個資料也會匯出以及 hello 裝置資料。 hello 下列範例示範這種格式。 Hello 最後 hello"twinETag"行中的所有資料都是兩個資料。

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

如果您需要存取 toothis 資料在程式碼中的，您可以輕鬆地還原序列化使用 hello 這個資料**ExportImportDevice**類別。 hello 下列 C# 程式碼片段示範如何 tooread 裝置資訊是先前匯出 tooa 區塊 blob:

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> 您也可以使用 hello **GetDevicesAsync**方法 hello **RegistryManager**類別 toofetch 您裝置的清單。 不過，這個方法會有 1000年硬上限 hello 裝置物件所傳回的數目。 hello 預期 hello 的使用案例**GetDevicesAsync**方法供開發案例 tooaid 偵錯並不建議在實際執行工作負載。

## <a name="import-devices"></a>匯入裝置

hello **ImportDevicesAsync**方法在 hello **RegistryManager**類別可讓您 tooperform 大量匯入和同步處理作業在 IoT hub 身分識別登錄中的。 像 hello **ExportDevicesAsync**方法、 hello **ImportDevicesAsync**方法會使用 hello**作業**架構。

小心使用 hello **ImportDevicesAsync**方法，因為在加法 tooprovisioning 新的裝置身分識別登錄中，同時，也更新並刪除現有的裝置。

> [!WARNING]
> 匯入操作是無法復原的。 一定要備份您現有的資料使用 hello **ExportDevicesAsync**方法 tooanother blob 容器進行大量變更 tooyour 身分識別登錄。

hello **ImportDevicesAsync**方法會採用兩個參數：

* A*字串*，其中包含的 URI [Azure 儲存體](../storage/index.md)blob 做為容器 toouse*輸入*toohello 作業。 此 URI 必須包含授與讀取權限 toohello 容器的 SAS 權杖。 此容器必須包含 hello 名稱的 blob **devices.txt** ，其中包含序列化 hello 裝置資料 tooimport 到您的身分識別登錄。 hello 匯入資料必須包含裝置資訊 hello 中相同的 JSON 格式的 hello **ExportImportDevice**會在建立時，工作會使用**devices.txt** blob。 hello SAS 權杖必須包含這些權限：

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* A*字串*，其中包含的 URI [Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)blob 做為容器 toouse*輸出*從 hello 作業。 hello 作業會建立區塊 blob 中此容器 toostore 任何錯誤資訊從 hello 完成匯入**作業**。 hello SAS 權杖必須包含這些權限：

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> hello 兩個參數可以指向 toohello 相同的 blob 容器。 hello 個別參數只會啟用更充分掌控您的資料為 hello 輸出容器需要其他權限。

hello 下列 C# 程式碼片段示範如何 tooinitiate 匯入工作：

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

這個方法也可以使用的 tooimport hello hello 裝置兩個資料。 hello hello 資料輸入格式為 hello 格式 hello 所示為 hello 相同**ExportDevicesAsync** > 一節。 如此一來，您可以重新匯入匯出的 hello 資料。 hello **$metadata**是選擇性的。

## <a name="import-behavior"></a>匯入行為

您可以使用 hello **ImportDevicesAsync**方法 tooperform hello 下列大量身分識別登錄中的作業：

* 大量註冊新裝置
* 大量刪除現有裝置
* 大量變更狀態 (啟用或停用裝置)
* 大量指派新的裝置驗證金鑰
* 大量自動重新產生裝置驗證金鑰
* 大量更新對應項資料

您可以執行 hello 之前在單一作業的任何組合**ImportDevicesAsync**呼叫。 例如，註冊新裝置和刪除或更新現有裝置 hello 在相同的時間。 當搭配 hello **ExportDevicesAsync**方法，從一個 IoT 中樞 tooanother 完全移轉您的裝置。

如果 hello 匯入檔案包含兩個中繼資料，此中繼資料會覆寫 hello 現有的兩個中繼資料。 如果 hello 匯入檔案未包含兩個中繼資料，然後只 hello`lastUpdateTime`使用 hello 目前的時間來更新中繼資料。

選擇性使用 hello **importMode** hello 匯入的序列化資料的每個裝置 toocontrol hello 匯入程序每個裝置中的屬性。 hello **importMode**屬性有下列選項的 hello:

| importMode | 說明 |
| --- | --- |
| **createOrUpdate** |如果裝置不存在指定的 hello**識別碼**，新註冊。 <br/>如果 hello 裝置已經存在，現有的資訊會覆寫，以提供的輸入的資料，而不考慮 toohello hello **ETag**值。 <br> hello 使用者可以選擇指定兩個資料，以及 hello 裝置資料。 兩個 hello 的 etag，如果指定，都是獨立處理從裝置 hello 的 etag。 如果沒有與 hello 現有兩個的 etag 不相符，錯誤會寫入 toohello 記錄檔。 |
| **create** |如果裝置不存在指定的 hello**識別碼**，新註冊。 <br/>如果 hello 裝置已經存在，錯誤會寫入 toohello 記錄檔。 <br> hello 使用者可以選擇指定兩個資料，以及 hello 裝置資料。 兩個 hello 的 etag，如果指定，都是獨立處理從裝置 hello 的 etag。 如果沒有與 hello 現有兩個的 etag 不相符，錯誤會寫入 toohello 記錄檔。 |
| **update** |如果裝置已經存在具有指定的 hello**識別碼**，會覆寫現有的資訊以提供的輸入的資料，而不考慮 toohello hello **ETag**值。 <br/>如果 hello 裝置不存在，錯誤會寫入 toohello 記錄檔。 |
| **pdateIfMatchETagu** |如果裝置已經存在具有指定的 hello**識別碼**，會覆寫現有的資訊以提供輸入的資料，只有當此時 hello **ETag**比對。 <br/>如果 hello 裝置不存在，錯誤會寫入 toohello 記錄檔。 <br/>如果沒有**ETag**不相符，會寫入錯誤 toohello 記錄檔。 |
| **createOrUpdateIfMatchETag** |如果裝置不存在指定的 hello**識別碼**，新註冊。 <br/>如果 hello 裝置已經存在，現有的資訊會覆寫，以提供輸入的資料，只有當此時 hello **ETag**比對。 <br/>如果沒有**ETag**不相符，會寫入錯誤 toohello 記錄檔。 <br> hello 使用者可以選擇指定兩個資料，以及 hello 裝置資料。 兩個 hello 的 etag，如果指定，都是獨立處理從裝置 hello 的 etag。 如果沒有與 hello 現有兩個的 etag 不相符，錯誤會寫入 toohello 記錄檔。 |
| **delete** |如果裝置已經存在具有指定的 hello**識別碼**，它會刪除，而不考慮 toohello **ETag**值。 <br/>如果 hello 裝置不存在，錯誤會寫入 toohello 記錄檔。 |
| **deleteIfMatchETag** |如果裝置已經存在具有指定的 hello**識別碼**，只有當此時刪除**ETag**比對。 如果 hello 裝置不存在，錯誤會寫入 toohello 記錄檔。 <br/>如果沒有 ETag 不符，錯誤會寫入 toohello 記錄檔。 |

> [!NOTE]
> 如果 hello 的序列化資料未明確定義**importMode**旗標的裝置，則預設太**createOrUpdate** hello 期間匯入作業。

## <a name="import-devices-example--bulk-device-provisioning"></a>匯入裝置範例 - 大量裝置佈建

hello 下列 C# 程式碼範例說明如何 toogenerate 多個裝置身分識別的：

* 包含驗證金鑰。
* 寫入該裝置資訊 tooa 區塊 blob。
* Hello 裝置匯入 hello 身分識別登錄。

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a>匯入裝置範例 - 大量刪除

hello 下列程式碼範例示範如何使用加入 toodelete hello 裝置 hello 上述程式碼範例：

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a>取得 hello 容器 SAS URI

hello 下列程式碼範例將示範如何 toogenerate [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)具有讀取、 寫入和刪除 blob 容器的權限：

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a>後續步驟

在本文中，您學會如何 tooperform 大量 IoT 中樞中的 hello 身分識別登錄作業。 請遵循這些連結 toolearn 更多關於管理 Azure IoT 中樞：

* [IoT 中樞度量][lnk-metrics]
* [作業監視][lnk-monitor]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [使用 IoT Edge 來模擬裝置][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
