---
title: "aaaUse 動態遙測 |Microsoft 文件"
description: "請遵循此教學課程 toolearn toouse 動態遙測 hello Azure IoT 套件遠端監視預先方案的設定。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>使用動態遙測以 hello 遠端監視預先設定的解決方案

動態遙測可讓您 toovisualize 任何傳送遙測 toohello 遠端監視預先設定的解決方案。 使用預先設定的 hello 方案部署的 hello 模擬裝置傳送氣溫和溼度遙測，您可以視覺化 hello 儀表板。 如果您自訂現有的模擬的裝置，建立新的模擬的裝置，或連接實體裝置 toohello 預先設定的解決方案，您可以傳送 hello 外部溫度、 RPM 或 windspeed 其他遙測等值。 然後，您可以視覺化這個 hello 儀表板上的其他遙測。

本教學課程使用簡單 Node.js 模擬的裝置，您可以輕鬆地修改 tooexperiment 與動態遙測。

toocomplete 本教學課程中，您將需要：

* 有效的 Azure 訂用帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。
* [Node.js][lnk-node] 0.12.x 版或更新版本。

您可以在任何作業系統上完成本教學課程，例如 Windows 或 Linux，只要您可以在其中安裝 Node.js。

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>新增遙測類型

hello 下一個步驟是由一組新的值與 hello Node.js 模擬裝置產生 tooreplace hello 遙測：

1. 輸入的停止 hello Node.js 模擬的裝置**Ctrl + C**在命令提示字元或殼層。
2. 在 hello remote_monitoring.js 檔案中，您可以看到 hello 現有溫度、 溼度，以及外部溫度遙測 hello 基底的資料值。 加入 **rpm** 的基底資料值，如下所示：

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. hello Node.js 模擬的裝置會使用 hello **generateRandomIncrement**函式在 hello remote_monitoring.js 檔案 tooadd 隨機遞增 toohello 基底的資料值。 隨機化 hello **rpm**值加入一行程式碼，請在 hello 現有隨機後，如下所示：

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. 加入 hello 新 rpm 值 toohello JSON 裝載 hello 裝置傳送 tooIoT 中樞：

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. 執行 hello Node.js 模擬的裝置使用 hello 下列命令：

    `node remote_monitoring.js`

6. 觀察在 hello 儀表板中的 hello 圖表顯示的 hello 新 RPM 遙測類型：

![新增 RPM toohello 儀表板][image3]

> [!NOTE]
> 您可能需要 toodisable，然後啟用 hello Node.js 裝置 hello**裝置**hello 儀表板 toosee hello 變更立即在頁面。

## <a name="customize-hello-dashboard-display"></a>自訂 hello 儀表板顯示

hello**裝置資訊**訊息可以包含中繼資料相關 hello 遙測 hello 裝置皆可傳送 tooIoT 中樞。 此中繼資料，可以指定 hello 裝置所傳送的 hello 遙測類型。 修改 hello **deviceMetaData**中 hello remote_monitoring.js 檔案 tooinclude 值**遙測**定義下列 hello**命令**定義。 hello 下列程式碼片段顯示 hello**命令**定義 (可確定 tooadd`,`之後 hello**命令**定義):

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> hello 遠端監視解決方案會使用不區分大小寫的相符項目 toocompare hello 中繼資料定義與 hello 遙測資料流中的資料。


加入**遙測**定義中所示 hello 上述程式碼片段不會變更 hello 儀表板的 hello 行為。 不過，也可以包含 hello 中繼資料**DisplayName**屬性 toocustomize hello 顯示 hello 儀表板中的。 更新 hello**遙測**中繼資料定義 hello 下列程式碼片段所示：

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

hello 下列螢幕擷取畫面顯示這項變更如何修改 hello hello 儀表板上的圖表圖例：

![自訂 hello 圖表圖例][image4]

> [!NOTE]
> 您可能需要 toodisable，然後啟用 hello Node.js 裝置 hello**裝置**hello 儀表板 toosee hello 變更立即在頁面。

## <a name="filter-hello-telemetry-types"></a>篩選 hello 遙測類型

根據預設，hello 儀表板上的 hello 圖表可顯示 hello 遙測資料流中的每個資料數列。 您可以使用 hello**裝置資訊**中繼資料 toosuppress hello hello 圖表上的特定遙測類型顯示。 

toomake hello 圖表顯示只有氣溫和溼度遙測，省略**ExternalTemperature**從 hello**裝置資訊****遙測**中繼資料，如下所示：

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

hello**室外溫度**不會再顯示 hello 圖表上：

![Hello 儀表板上的篩選器 hello 遙測][image5]

這項變更只會影響 hello 圖表顯示。 hello **ExternalTemperature**資料值仍會儲存並可供任何後端處理。

> [!NOTE]
> 您可能需要 toodisable，然後啟用 hello Node.js 裝置 hello**裝置**hello 儀表板 toosee hello 變更立即在頁面。

## <a name="handle-errors"></a>處理錯誤

如 hello 圖表上的資料流 toodisplay 其**類型**在 hello**裝置資訊**中繼資料必須符合 hello hello 遙測值資料型別。 例如，如果 hello 中繼資料會指定該 hello**類型**溼度的資料是**int**和**雙**則 hello 溼度遙測不會位於 hello 遙測資料流不會顯示 hello 圖表上。 不過，hello**溼度**值仍會儲存並可供任何後端處理。

## <a name="next-steps"></a>後續步驟

既然您已經看到如何 toouse 動態遙測，您可以了解 hello 預先設定的解決方案如何使用裝置資訊： [hello 遠端監視裝置資訊的中繼資料已預先設定的解決方案][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
