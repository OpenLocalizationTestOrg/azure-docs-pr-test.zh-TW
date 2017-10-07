---
title: "aaaDevice 資訊的中繼資料中 hello 遠端監視解決方案 |Microsoft 文件"
description: "Hello 預先設定的 Azure IoT 解決方案遠端監視和其結構描述。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>裝置資訊的中繼資料中 hello 遠端監視預先設定的解決方案

hello Azure IoT 套件遠端監視預先設定的解決方案示範管理裝置的中繼資料的方法。 本文將概述 hello 方法此解決方案會 tooenable 您 toounderstand:

* 會儲存哪些裝置中繼資料 hello 解決方案。
* Hello 方案管理 hello 裝置中繼資料的方式。

## <a name="context"></a>Context

hello 遠端監視預先設定的解決方案會使用[Azure IoT 中樞][ lnk-iot-hub] tooenable 您裝置 toosend 資料 toohello 雲端。 hello 方案會在三個不同的位置儲存裝置的相關資訊：

| 位置 | 儲存的資訊 | 實作 |
| -------- | ------------------ | -------------- |
| 身分識別登錄 | 裝置識別碼、驗證金鑰和啟用狀態 | 內建的 tooIoT 中樞 |
| 裝置對應項 | 中繼資料：報告屬性、所需屬性、標記 | 內建的 tooIoT 中樞 |
| Cosmos DB | 命令和方法歷程記錄 | 針對解決方案自訂 |

IoT 中樞包含[裝置身分登錄][ lnk-identity-registry] toomanage 存取 tooan IoT 中樞，並使用[裝置雙][ lnk-device-twin] toomanage 裝置中繼資料. 還有遠端監視解決方案專用*裝置登錄*可儲存命令和方法歷程記錄。 遠端監視解決方案使用 hello [Cosmos DB] [ lnk-docdb]資料庫 tooimplement 命令和方法的歷程記錄的自訂存放區。

> [!NOTE]
> hello 遠端監視預先設定的解決方案會保留 hello 裝置身分登錄與 hello 資訊同步 hello Cosmos DB 資料庫中。 兩者都使用相同的裝置識別碼 toouniquely 識別的 hello 連接 tooyour IoT 中樞的每個裝置。

## <a name="device-metadata"></a>裝置中繼資料

IoT 中樞維護[裝置兩個][ lnk-device-twin]針對每個模擬與實體裝置連線 tooa 遠端監視解決方案。 hello 解決方案會使用裝置雙 toomanage hello 中繼資料與裝置相關聯。 裝置的兩個是由 IoT 中樞維護的 JSON 文件和 hello 方案會使用裝置雙 hello IoT 中樞 API toointeract。

裝置對應項可儲存三種中繼資料︰

- *報告內容*tooan IoT 中樞傳送的裝置。 Hello 遠端監視解決方案，在模擬的裝置傳送報告的內容在啟動時，以回應太**變更裝置狀態**命令和方法。 您可以檢視報告的內容中 hello**裝置清單**和**裝置詳細資料**hello 方案入口網站中。 報告屬性是唯讀的。
- *所需屬性*取自裝置 hello IoT 中樞。 它負責 hello hello 裝置 toomake hello 裝置的任何必要的組態變更。 它也是做為報告屬性 hello 裝置 tooreport hello 變更後 toohello 中樞 hello 責任。 您可以設定透過 hello 方案入口網站所需的屬性值。
- *標記*只存在於 hello 裝置兩個，並永遠不會與裝置同步處理。 您可以在 hello 方案入口網站設定標記值，並使用它們，當您篩選 hello 的裝置清單。 hello 解決方案也會使用標記 tooidentify hello 圖示 toodisplay hello 方案入口網站中的裝置。

範例會報告從 hello 模擬裝置的屬性包括製造商、 型號、 緯度與經度。 模擬的裝置也會傳回 hello 清單支援的方法做為報告的屬性。

> [!NOTE]
> hello 模擬的裝置的程式碼只會使用 hello **Desired.Config.TemperatureMeanValue**和**Desired.Config.TelemetryInterval**需的屬性 tooupdate hello 報告傳送回屬性tooIoT 中樞。 所有其他所需屬性變更要求都會被忽略。

裝置資訊的中繼資料 JSON 文件儲存在 hello 裝置登錄 Cosmos DB 資料庫具有下列結構的 hello:

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> 裝置資訊也可以包含中繼資料 toodescribe hello 遙測 hello 裝置傳送 tooIoT 中樞。 hello 遠端監視解決方案會使用這個 hello 儀表板的顯示方式的遙測中繼資料 toocustomize[動態遙測][lnk-dynamic-telemetry]。

## <a name="lifecycle"></a>生命週期

當您第一次可以建立裝置 hello 方案入口網站中時，hello 方案建立 hello Cosmos DB 資料庫 toostore 命令中的項目和方法歷程記錄。 此時，hello 解決方案也會建立 hello 裝置項目在 hello 裝置身分識別登錄中，會產生 hello 金鑰 hello 裝置使用 tooauthenticate 與 IoT 中樞。 它也會建立裝置對應項。

當裝置第一次連接 toohello 方案時，它會傳送報告的屬性和裝置資訊訊息。 hello 報告屬性值會自動儲存在 hello 裝置兩個。 hello 報告屬性包括 hello 裝置製造商、 型號、 序號和支援的方法清單。 hello 裝置資訊訊息包含 hello hello 裝置支援包括任何命令參數的相關資訊的 hello 命令清單。 Hello 方案收到此訊息時，它會更新 hello hello Cosmos DB 資料庫中的裝置資訊。

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>檢視和編輯 hello 方案入口網站中的裝置資訊

hello hello 方案入口網站中的 [裝置] 清單會顯示下列資料行的裝置屬性，預設的 hello:**狀態**， **DeviceId**，**製造商**， **型號**，**序號**，**韌體**，**平台**，**處理器**，和**安裝 RAM**。 您可以按一下自訂 hello 行**資料行編輯器**。 hello 裝置屬性**緯度**和**經度**hello 儀表板上的磁碟機 hello Bing 地圖中的 hello 位置。

![裝置清單中的資料行編輯器][img-device-list]

在 hello**裝置詳細資料**窗格在 hello 方案入口網站中，您可以編輯所需的屬性和標記 （報告屬性唯讀）。

![裝置詳細資料窗格][img-device-edit]

您可以從您的方案使用 hello 方案入口網站 tooremove 裝置。 當您移除裝置時，hello 方案會從身分識別登錄移除 hello 裝置項目，然後再刪除 hello 裝置兩個。 hello 解決方案也會從 hello Cosmos DB 資料庫移除資訊相關的 toohello 裝置。 您必須先停用裝置，才可以將它移除。

![移除裝置][img-device-remove]

## <a name="device-information-message-processing"></a>裝置資訊訊息處理

裝置所傳送的裝置資訊訊息與遙測訊息不同。 裝置資訊訊息包括裝置可回應 hello 命令和任何命令歷程記錄。 IoT 中樞本身並不了解包含裝置資訊訊息中的 hello 中繼資料和處理序 hello 中 hello 訊息處理的任何裝置到雲端訊息的方式相同。 在遠端監視解決方案，hello [Azure Stream Analytics] [ lnk-stream-analytics] (ASA) 作業會從 IoT 中樞讀取 hello 訊息。 hello **DeviceInfo** stream analytics 工作包含的訊息篩選條件**"ObjectType":"DeviceInfo"**並將它們轉送 toohello **EventProcessorHost**主機web 工作中執行的執行個體。 Hello 中的邏輯**EventProcessorHost**執行個體會使用 hello 特定裝置與更新 hello 記錄 hello 裝置識別碼 toofind hello Cosmos DB 記錄。

> [!NOTE]
> 裝置資訊訊息是標準的裝置對雲端訊息。 hello 方案區分裝置的資訊訊息和遙測訊息使用 ASA 查詢。

## <a name="next-steps"></a>後續步驟

現在您已完成學習如何自訂 hello 預先設定的解決方案，您可以瀏覽 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [預先設定的預防性維護解決方案概觀][lnk-predictive-overview]
* [IoT 套件的常見問題集][lnk-faq]
* [從 hello 接地 IoT 安全性][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
