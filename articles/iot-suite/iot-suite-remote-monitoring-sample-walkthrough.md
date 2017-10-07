---
title: "逐步解說中預先設定的監視解決方案 aaaRemote |Microsoft 文件"
description: "Hello 預先設定的 Azure IoT 解決方案遠端監視和其結構描述。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>遠端監視預先設定解決方案逐步解說

hello IoT 套件遠端監視[預先設定的解決方案][ lnk-preconfigured-solutions]的端對端實作監視多部電腦執行遠端位置中的方案。 hello 解決方案結合主要 Azure 服務 tooprovide hello 的商務案例的泛型實作。 您可以做為起點使用 hello 解決方案，為您自己的實作和[自訂][ lnk-customize]它 toomeet 特定的業務需求。

本文將引導您完成一些 hello hello 遠端監視解決方案 tooenable 的索引鍵項目您 toounderstand 它的運作方式。 這項知識能協助您︰

* 疑難排解 hello 方案中的問題。
* 規劃如何 toocustomize toohello 方案 toomeet 您自己的特定需求。 
* 設計使用 Azure 服務的 IoT 解決方案。

## <a name="logical-architecture"></a>邏輯架構

下列圖表中的 hello 概述 hello 邏輯解決方案元件的預先設定的 hello:

![邏輯架構](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>模擬的裝置

預先設定的 hello 方案中 hello 模擬的裝置會代表冷卻裝置 （例如建置冷氣或設備空氣處理單元中）。 當您部署預先設定的 hello 方案時，您也會自動佈建執行中的四個模擬的裝置[Azure WebJob][lnk-webjobs]。 hello 模擬裝置方便您 tooexplore hello 方案行為的 hello hello 需要 toodeploy 沒有任何實體裝置。 toodeploy 實際實體裝置，請參閱 hello[連接您的裝置 toohello 遠端監視預先設定的解決方案][ lnk-connect-rm]教學課程。

### <a name="device-to-cloud-messages"></a>裝置到雲端的訊息

每個模擬的裝置皆可傳送下列訊息類型 tooIoT 中樞 hello:

| 訊息 | 說明 |
| --- | --- |
| 啟動 |Hello 裝置啟動時，它會傳送**裝置資訊**toohello 後端包含與其本身相關的資訊訊息。 此資料包含 hello 裝置識別碼和 hello 命令的清單，而且方法 hello 裝置支援。 |
| 目前狀態 |裝置會定期傳送**存在**訊息 tooreport 是否 hello 裝置可以有意義的感應器的 hello 存在。 |
| 遙測 |裝置會定期傳送**遙測**報告模擬的值，如 hello 氣溫和溼度從 hello 裝置收集到的訊息的模擬感應器。 |

> [!NOTE]
> hello 方案會儲存 hello hello 裝置 Cosmos DB 資料庫中，而不是在 hello 裝置兩個支援的命令清單。

### <a name="properties-and-device-twins"></a>屬性和裝置對應項

hello 模擬的裝置傳送 hello 下列裝置屬性 toohello[兩個][ lnk-device-twins]在 hello IoT 中樞與*報告屬性*。 hello 裝置傳送報告屬性，在啟動和回應 tooa**變更裝置狀態**命令或方法。

| 屬性 | 目的 |
| --- | --- |
| Config.TelemetryInterval | 頻率 （秒） hello 裝置傳送遙測 |
| Config.TemperatureMeanValue | 指定模擬的 hello 溫度遙測 hello 平均值 |
| Device.DeviceID |提供或裝置 hello 方案中建立時指派的識別碼 |
| Device.DeviceState | Hello 裝置所報告的狀態 |
| Device.CreatedTime |建立時間 hello 裝置 hello 方案中 |
| Device.StartupTime |啟動時間 hello 裝置 |
| Device.LastDesiredPropertyChange |hello 版本號碼的 hello 最後所需的屬性變更 |
| Device.Location.Latitude |緯度 hello 裝置位置 |
| Device.Location.Longitude |經度 hello 裝置位置 |
| System.Manufacturer |裝置製造商 |
| System.ModelNumber |Hello 裝置的模型數目 |
| System.SerialNumber |Hello 裝置的序號 |
| System.FirmwareVersion |目前在 hello 裝置上的韌體版本 |
| System.Platform |Hello 裝置的平台架構 |
| System.Processor |處理器執行中的 hello 裝置 |
| System.InstalledRAM |Hello 裝置上安裝的 RAM 數量 |

hello 模擬器植入模擬裝置的範例值中的這些屬性。 每次 hello 模擬器初始化模擬的裝置、 裝置 hello 報告 hello 預先定義的中繼資料 tooIoT 中樞為報告的屬性。 報告的屬性只能由 hello 裝置更新。 toochange 報告屬性，您想要的屬性中設定方案入口網站。 負責 hello hello 裝置：

1. 定期擷取 hello IoT 中樞所需的屬性。
2. 包含所需的 hello 屬性值更新其設定。
3. 以報告屬性，傳送 hello 新值後 toohello 中樞。

從 hello 方案儀表板，您可以使用*所需屬性*tooset 屬性上的裝置使用 hello[裝置兩個][lnk-device-twins]。 一般而言，裝置會從回時報告屬性，變更其內部狀態和報告 hello hello 中樞 tooupdate 讀取所需的屬性值。

> [!NOTE]
> hello 模擬的裝置的程式碼只會使用 hello **Desired.Config.TemperatureMeanValue**和**Desired.Config.TelemetryInterval**需的屬性 tooupdate hello 報告傳送回屬性tooIoT 中樞。 所有其他想要的屬性變更要求會遭到忽略 hello 模擬的裝置。

### <a name="methods"></a>方法

hello 模擬的裝置可以處理下列方法 hello ([直接方法][lnk-direct-methods]) 從 hello 方案入口網站來完成 hello IoT 中樞叫用：

| 方法 | 說明 |
| --- | --- |
| InitiateFirmwareUpdate |指示 hello 裝置 tooperform 韌體更新 |
| 重新啟動 |指示 hello 裝置 tooreboot |
| FactoryReset |指示 hello 裝置 tooperform 原廠重設 |

有些方法會使用進度報告的內容 tooreport。 例如，hello **InitiateFirmwareUpdate**方法模擬 hello 裝置上以非同步方式執行 hello 更新。 hello 方法會立即傳回 hello 在裝置上，同時 hello 非同步工作會繼續 toosend 狀態更新回 toohello 方案儀表板中使用報告的屬性。

### <a name="commands"></a>命令

hello 模擬裝置可以處理下列命令 （雲端到裝置訊息） 從 hello 方案入口網站來完成 hello IoT 中樞傳送的 hello:

| 命令 | 說明 |
| --- | --- |
| PingDevice |傳送*ping* toohello 裝置 toocheck 是保持運作 |
| StartTelemetry |啟動 hello 裝置傳送遙測 |
| StopTelemetry |停駐點 hello 裝置傳送遙測 |
| ChangeSetPointTemp |變更 hello 設定點值周圍的 hello 隨機產生的資料 |
| DiagnosticTelemetry |觸發程序 hello 裝置模擬器 toosend 其他遙測值 (externalTemp) |
| ChangeDeviceState |變更裝置 hello 擴充的狀態屬性並從 hello 裝置傳送 hello 裝置資訊訊息 |

> [!NOTE]
> 如需這些命令 (雲端到裝置訊息) 和方法 (直接方法) 的比較，請參閱[雲端到裝置通訊指引][lnk-c2d-guidance]。

## <a name="iot-hub"></a>IoT 中樞

hello [IoT 中樞][ lnk-iothub]內嵌到 hello 雲端從 hello 裝置傳送資料，並使其成為可用 toohello Azure 資料流分析 (ASA) 作業。 每個資料流 ASA 工作會使用個別的 IoT 中樞取用者群組 tooread hello 訊息資料流從您的裝置。

也 hello hello 方案中的 IoT 中樞：

- 維護儲存 hello 識別碼和驗證金鑰允許 tooconnect toohello 入口網站的所有 hello 裝置身分識別登錄。 您可以啟用和停用透過 hello 身分識別登錄的裝置。
- 命令 tooyour 裝置的身分將傳送嗨方案入口網站。
- 代表 hello 方案入口網站來叫用您的裝置上的方法。
- 維護所有已註冊裝置的裝置對應項。 裝置的兩個儲存報告的裝置 hello 屬性值。 裝置的兩個也會儲存所需的屬性，在 hello 方案入口網站的 hello 裝置 tooretrieve 接下來連接時設定。
- 排程工作的多個裝置的 tooset 屬性，或叫用多個裝置上的方法。

## <a name="azure-stream-analytics"></a>Azure 串流分析

在遠端監視解決方案，hello [Azure Stream Analytics] [ lnk-asa] (ASA) 會將收到 hello IoT 中樞 tooother 後端元件進行處理或儲存體裝置訊息發送。 不同 ASA 工作執行的 hello 訊息 hello 內容為基礎的特定功能。

**工作 1： 裝置資訊**篩選從 hello 內送訊息資料流的裝置資訊訊息，並將它們傳送 tooan 事件中樞端點。 裝置傳送郵件的裝置資訊，在啟動和回應 tooa **SendDeviceInfo**命令。 此工作會使用下列查詢定義 tooidentify hello**裝置資訊**訊息：

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

這項作業會傳送其輸出 tooan 事件中心的進一步處理。

**作業 2：規則** 會針對每一裝置臨界值評估傳入氣溫和溼度遙測值。 在 hello hello 方案入口網站中提供的規則編輯器中設定臨界值。 每個裝置/值組是依據時間戳記儲存在 blob 中，串流分析會讀取做為 **參考資料**。 hello 工作比較 hello 裝置 hello 設定的閾值對任何非空白的值。 如果它超過 hello ' >' 條件，hello 工作輸出**警示**超過事件，表示該 hello 臨界值，並提供裝置 hello、 值和時間戳記值。 此工作會使用下列查詢定義 tooidentify 遙測訊息應該會觸發警示的 hello:

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

hello 工作會傳送其輸出 tooan 事件中心的進一步處理，其中 hello 方案入口網站可以讀取 hello 警示資訊會儲存每個警示 tooblob 儲存體的詳細資料。

**工作 3： 遙測**hello 傳入裝置遙測資料流上兩種方式運作。 hello 第一次傳送遙測的所有訊息從 hello 裝置 toopersistent blob 儲存體進行長期儲存。 hello 第二個計算平均值、 最小值和最大溼度值經過五分鐘滑動視窗，並傳送這個資料 tooblob 儲存體。 hello 方案入口網站會讀取 blob 儲存體 toopopulate hello 圖表中的 hello 遙測資料。 此工作會使用下列查詢定義的 hello:

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>事件中樞

hello**裝置資訊**和**規則**ASA 工作輸出及其資料 tooEvent 集線器 tooreliably 向前上 toohello**事件處理器**hello WebJob 中執行。

## <a name="azure-storage"></a>Azure 儲存體

hello 解決方案會使用 Azure blob 儲存體 toopersist 所有 hello 原始和摘要遙測資料從 hello 裝置 hello 方案中。 hello 入口網站會讀取 blob 儲存體 toopopulate hello 圖表中的 hello 遙測資料。 toodisplay 警示 hello 方案入口網站，讀取 hello blob 儲存體記錄的遙測值超過 hello 設定臨界值時。 hello 解決方案也會使用 blob 儲存體 toorecord hello 臨界值 hello 方案入口網站中設定。

## <a name="webjobs"></a>WebJobs

此外 toohosting hello 裝置模擬器都會 hello WebJobs hello 方案中也主機 hello**事件處理器**Azure WebJob 會處理命令的回應中執行。 它會使用命令的回應訊息 tooupdate hello 裝置命令歷程記錄 （儲存在 hello Cosmos DB 資料庫）。

## <a name="cosmos-db"></a>Cosmos DB

hello 解決方案會使用 Cosmos DB 資料庫 toostore 需 hello 裝置連線的 toohello 解決方案資訊。 這項資訊包括 hello 歷程記錄從 hello 方案入口網站傳送 toodevices 命令和叫用從 hello 方案入口網站的方法。

## <a name="solution-portal"></a>解決方案入口網站

hello 方案入口網站是 web 應用程式部署成預先設定的 hello 方案的一部分。 hello 方案入口網站中的 hello 金鑰頁面是 hello 儀表板和 hello 裝置清單。

### <a name="dashboard"></a>儀表板

此頁面在 hello web 應用程式會使用 PowerBI javascript 控制項 (請參閱[PowerBI 視覺效果儲存機制](https://www.github.com/Microsoft/PowerBI-visuals)) hello 裝置 toovisualize hello 遙測資料。 hello 解決方案會使用 hello ASA 遙測工作 toowrite hello 遙測資料 tooblob 儲存區。

### <a name="device-list"></a>裝置清單

您可以從這個頁面在 hello 方案入口網站：

* 佈建新裝置。 此動作設定 hello 唯一裝置識別碼，並會產生 hello 驗證金鑰。 它會寫入 hello 裝置 tooboth hello IoT 中樞身分識別登錄的相關資訊與 hello 解決方案專用 Cosmos DB 資料庫。
* 管理裝置屬性。 這個動作包括檢視現有屬性和使用新的屬性更新。
* 傳送命令 tooa 裝置。
* 檢視裝置 hello 命令歷程記錄。
* 啟用和停用裝置。

## <a name="next-steps"></a>後續步驟

hello 下列 TechNet 部落格文章提供更多詳細 hello 遠端監視預先設定的解決方案：

* [IoT 套件下 hello 其實-遠端監視](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT 套件 - 遠端監視 - 新增即時與模擬裝置](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

您可以繼續閱讀下列文章 hello 入門 IoT 套件：

* [連接您的裝置 toohello 遠端監視預先設定的解決方案][lnk-connect-rm]
* [Hello azureiotsuite.com 網站的權限][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
