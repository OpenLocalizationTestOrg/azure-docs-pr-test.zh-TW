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
# <a name="customize-a-preconfigured-solution"></a>自訂預先設定的方案

hello Azure IoT 套件所隨附的預先設定的 hello 解決方案示範 hello 套件工作一起 toodeliver 端對端方案中的 hello 服務。 從這個起點，有不同的位置中，您可以擴充和自訂用於特定案例的 hello 方案。 hello 下列各節說明這些常見的自訂點。

## <a name="find-hello-source-code"></a>尋找 hello 原始程式碼

hello 來源的預先設定的 hello 解決方案會提供程式碼在 GitHub 上遵循儲存機制的 hello:

* 遠端監視： [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* 預測性維護︰ [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* 已連線的處理站︰[https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

toodemonstrate hello 模式和實務用 tooimplement hello 端對端功能的 IoT 解決方案使用 Azure IoT 套件係 hello 原始程式碼 hello 預先設定的解決方案。 您可以找到更多有關 toobuild 及部署 hello GitHub 儲存機制中的 hello 方案。

## <a name="change-hello-preconfigured-rules"></a>變更 hello 預先設定規則

hello 遠端監視解決方案包括三個[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) toohandle 裝置資訊、 遙測以及在 hello 方案中的規則邏輯的工作。

hello 三個資料流分析工作和其語法所述的 hello 深度[遠端監視預先設定的方案逐步解說](iot-suite-remote-monitoring-sample-walkthrough.md)。 

直接 tooalter hello 邏輯，或新增邏輯特定 tooyour 案例中，您可以編輯這些作業。 您可以找到 hello 串流分析工作，如下所示：

1. 跳過[Azure 入口網站](https://portal.azure.com)。
2. 瀏覽以相同的名稱，為您的 IoT 解決方案 hello toohello 資源群組。 
3. 選取您想要 toomodify hello Azure Stream Analytics 工作。 
4. 停止選取的 hello 工作**停止**在 hello 組命令。 
5. 編輯 hello 輸入、 查詢和輸出。
   
    簡單的修改是 hello toochange hello 查詢**規則**作業 toouse **"<"**而不是**">"**。 hello 方案入口網站仍會顯示**">"**當您編輯規則，但是請注意 hello 行為翻轉到期 toohello hello 基礎作業變更的方式。
6. 啟動 hello 工作

> [!NOTE]
> hello 遠端的監視儀表板取決於特定資料，因此改變 hello 作業可能會導致 hello 儀表板 toofail。

## <a name="add-your-own-rules"></a>新增自己的規則

此外 toochanging hello 預先設定 Azure 串流分析工作，您可以使用 hello Azure 入口網站 tooadd 新作業，或新增新的查詢 tooexisting 工作。

## <a name="customize-devices"></a>自訂裝置

其中一個 hello 最常見的延伸模組活動使用裝置特定 tooyour 案例。 使用裝置的方法有數種。 這些方法包括變更模擬的裝置 toomatch 案例中，或使用 hello [IoT 裝置 SDK] [ IoT Device SDK] tooconnect 實體裝置 toohello 方案。

逐步指南 tooadding 裝置，請參閱 hello [Iot 套件連接裝置](iot-suite-connecting-devices.md)發行項與 hello[遠端監視 sdk > 範例的 C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring)。 這個範例是以 hello 遠端監視預先設定的解決方案設計的 toowork。

### <a name="create-your-own-simulated-device"></a>建立自己的模擬裝置

包含在 hello[遠端監視解決方案原始程式碼](https://github.com/Azure/azure-iot-remote-monitoring)，是.NET 模擬器。 這個模擬器為 hello 佈建為一部分 hello 方案，而且您可以加以更改 toosend 不同的中繼資料，遙測，並回應 toodifferent 命令和方法的其中一個。

hello 遠端監視預先設定的解決方案中的 hello 預先設定的模擬器模擬冷卻器裝置發出氣溫和溼度的遙測。 您可以修改在 hello hello 模擬器[Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob)專案時，您已分叉 hello GitHub 儲存機制。

### <a name="available-locations-for-simulated-devices"></a>模擬裝置的可用位置

西雅圖/Redmond、 Washington、 美國政府正在 hello 預設集合的位置。 您可以在 [SampleDeviceFactory.cs][lnk-sample-device-factory] 變更這些位置。

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>加入所需的屬性更新處理常式 toohello 模擬器

您可以在 hello 方案入口網站中設定裝置所需屬性的值。 它負責 hello hello 裝置 toohandle hello 屬性的變更要求時 hello 裝置擷取所需的 hello 屬性值。 屬性值變更為 tooadd 支援透過所需的屬性，您需要 tooadd 處理常式 toohello 模擬器。

hello 模擬器包含 hello 的處理常式**SetPointTemp**和**TelemetryInterval**屬性，您可以藉由設定更新預期 hello 方案入口網站中的值。

hello 下列範例顯示 hello 處理常式 hello **SetPointTemp**預期屬性在 hello **CoolerDevice**類別：

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

這個方法會更新 hello 遙測點溫度，然後報告 hello 變更後 tooIoT 中樞設定報告的屬性。

您可以在 hello 前面範例中的下列 hello 模式所為您自己的屬性加入自己的處理常式。

您也必須繫結 hello 所需的屬性 toohello 處理常式中 hello 下列從 hello 範例所示**CoolerDevice**建構函式：

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

請注意，**SetPointTempPropertyName** 是定義為 "Config.SetPointTemp" 的常數。

### <a name="add-support-for-a-new-method-toohello-simulator"></a>加入新的方法 toohello 模擬器的支援

您可以自訂的新 hello 模擬器 tooadd 支援[方法 （直接的方法）][lnk-direct-methods]。 有兩個必備主要步驟︰

- hello 模擬器必須通知 hello IoT 中樞 hello 預先設定的方案中使用 hello 方法詳細資料。
- hello 模擬器必須包含程式碼 toohandle hello 方法呼叫，當您叫用它從 hello**裝置詳細資料**hello 方案總管 中，或透過在工作面板。

hello 遠端監視預先設定的解決方案會使用*報告屬性*toosend 的支援的方法 tooIoT 集線器的詳細資料。 hello 方案後端會維護一份所有支援的方法引動過程的歷程記錄以及每個裝置的 hello 方法。 您可以檢視此裝置的相關資訊，並叫用 hello 方案入口網站中的方法。

toonotify hello IoT 中樞裝置支援的方法，hello 裝置必須加入詳細資料的 hello 方法 toohello **SupportedMethods** hello 中的節點回報屬性：

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

hello 方法簽章具有下列格式的 hello: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`。 例如，toospecify hello **InitiateFirmwareUpdate**方法必須要有字串參數名稱為**FwPackageURI**，使用下列方法簽章的 hello:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

如需支援的參數類型的清單，請參閱 hello **CommandTypes** hello 基礎結構的專案中的類別。

toodelete 方法，設定 hello 方法簽章太`null`hello 中報告的屬性。

> [!NOTE]
> hello 方案後端只會更新支援的方法的相關資訊時接收*裝置資訊*從裝置 hello 訊息。

下列程式碼範例的 hello hello **SampleDeviceFactory**類別中 hello 通用專案顯示如何 tooadd 方法 toohello 清單的**SupportedMethods** hello 中報告傳送嗨屬性裝置：

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

此程式碼片段加入詳細資料的 hello **InitiateFirmwareUpdate**包括文字 toodisplay hello 方案入口網站與 hello 的詳細資料的方法所需的方法參數。

hello 模擬器會傳送報告的屬性，包括 hello 的清單支援的方法，tooIoT hello 模擬器啟動時的中樞。

新增支援每個方法的處理常式 toohello 模擬器程式碼。 您可以看到 hello hello 中的現有處理常式**CoolerDevice** hello Simulator.WebJob 專案中的類別。 hello 下列範例顯示 hello 處理常式**InitiateFirmwareUpdate**方法：

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

方法的處理常式名稱開頭必須`On`後面接著 hello hello 方法名稱。 hello **methodRequest**參數會包含從 hello 方案後端以 hello 方法引動過程傳遞任何參數。 hello 傳回值必須是型別**工作&lt;MethodResponse&gt;**。 hello **BuildMethodResponse**公用程式方法，可協助您建立 hello 傳回值。

內部 hello 方法處理常式，您可以：

- 啟動非同步工作。
- 擷取所需的屬性從 hello*裝置兩個*在 IoT 中樞。
- 更新單一報告的屬性使用 hello **SetReportedPropertyAsync**方法在 hello **CoolerDevice**類別。
- 更新多個報告的屬性，藉由建立**TwinCollection**執行個體及呼叫 hello **Transport.UpdateReportedPropertiesAsync**方法。

hello 前例的韌體更新會執行下列步驟的 hello:

- 檢查 hello 裝置是無法 tooaccept hello 韌體更新要求。
- 以非同步方式起始 hello 韌體更新作業，而且 hello 作業完成時，會重設 hello 遙測。
- 立即傳回 hello"FirmwareUpdate 接受 」 訊息 tooindicate hello 要求接受 hello 裝置。

### <a name="build-and-use-your-own-physical-device"></a>建置並使用自己的 (實體) 裝置

hello [Azure IoT Sdk](https://github.com/Azure/azure-iot-sdks) IoT 解決方案，提供用於連接多個裝置類型 （語言和作業系統） 的程式庫。

## <a name="modify-dashboard-limits"></a>修改儀表板限制

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>儀表板下拉式清單中顯示的裝置數目

hello 預設值為 200。 您可以在 [DashboardController.cs][lnk-dashboard-controller] 變更這個數字。

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>在 Bing 地圖控制項中的 pin toodisplay 的數目

hello 預設值為 200。 您可以在 [TelemetryApiController.cs][lnk-telemetry-api-controller-01] 變更這個數字。

### <a name="time-period-of-telemetry-graph"></a>遙測圖形的期間

hello 預設值為 10 分鐘。 您可以在 [TelmetryApiController.cs][lnk-telemetry-api-controller-02] 變更此值。

## <a name="manually-set-up-application-roles"></a>手動設定應用程式角色

hello 下列程序描述如何 tooadd **Admin**和**ReadOnly**應用程式角色 tooa 預先設定的解決方案。 請注意，佈建 hello azureiotsuite.com 站台已預先設定的解決方案包括 hello **Admin**和**ReadOnly**角色。

成員的 hello **ReadOnly**角色可以看到 hello 儀表板和 hello 裝置清單中，但不是允許有 tooadd 裝置、 變更裝置的屬性或傳送命令。  成員的 hello **Admin**角色擁有完整存取 tooall hello 功能 hello 方案中。

1. 移 toohello [Azure 傳統入口網站][lnk-classic-portal]。
2. 選取 **Active Directory**。
3. 按一下 hello 您佈建您的方案時所使用的 hello AAD 租用戶名稱。
4. 按一下 [應用程式] 。
5. 按一下 hello 符合預先設定的方案名稱 hello 應用程式名稱。 如果您沒有看到您的應用程式，在 [hello] 清單中，選取**我公司所擁有的應用程式**在 hello**顯示**下拉式清單中，然後按一下 hello 核取記號。
6. 在 hello hello 頁面底部，按一下**管理資訊清單**然後**下載資訊清單**。
7. 此程序下載.json 檔案 tooyour 本機電腦。 使用您選擇的文字編輯器開啟此檔案並加以編輯。
8. 在 hello.json 檔案 hello 第三行，您可以看到：

   ```json
   "appRoles" : [],
   ```
   這一行取代為下列程式碼的 hello:

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

9. 儲存 hello 更新的.json 檔案 （您可以覆寫現有檔案的 hello）。
10. 在 hello Azure 傳統入口網站底部 hello hello 頁面上，選取 **管理資訊清單**然後**上傳資訊清單**tooupload hello 上一個步驟中儲存的 hello.json 檔案。
11. 您現在已新增 hello **Admin**和**ReadOnly**角色 tooyour 應用程式。
12. 其中一個在您目錄中，這些角色 tooa 使用者 tooassign 看到[hello azureiotsuite.com 網站的權限][lnk-permissions]。

## <a name="feedback"></a>意見反應

您有的自訂，您希望本文件涵蓋的 toosee 嗎？ 新增功能建議太[User Voice](https://feedback.azure.com/forums/321918-azure-iot)，或針對本文的註解。 

## <a name="next-steps"></a>後續步驟

toolearn 進一步了解 hello 選項自訂 hello 預先設定的解決方案，請參閱：

* [連接邏輯應用程式 tooyour Azure IoT 套件遠端監視預先設定的解決方案][lnk-logicapp]
* [使用動態遙測以 hello 遠端監視預先設定的解決方案][lnk-dynamic]
* [裝置資訊的中繼資料中 hello 遠端監視預先設定的解決方案][lnk-devinfo]
* [自訂 hello 從 OPC UA 伺服器所連接的原廠方案顯示資料][lnk-cf-customize]

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