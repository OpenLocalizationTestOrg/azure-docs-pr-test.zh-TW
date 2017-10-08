---
title: "IoT 中樞裝置到雲端 aaaAzure 選項 |Microsoft 文件"
description: "開發人員指南-當 toouse 裝置到雲端訊息、 報告的屬性或檔案上傳雲端到裝置通訊的指引。"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Device-to-cloud communications guidance
將資訊傳送從 hello 裝置應用程式 toohello 方案後端，IoT 中樞會公開三個選項：

* [裝置到雲端訊息][lnk-d2c]，適用於時間序列遙測和警示。
* [報告內容][ lnk-twins]報告裝置狀態資訊，例如可用的功能、 條件或 hello 的長時間執行工作流程的狀態。 例如，組態和軟體更新。
* [檔案上傳][ lnk-fileupload]媒體檔案和大型遙測批次上傳間斷連接裝置，或壓縮的 toosave 頻寬。

以下是 hello 的詳細的比較裝置到雲端通訊的各種選項。

|  | 裝置到雲端的訊息 | 報告屬性 | 檔案上傳 |
| ---- | ------- | ---------- | ---- |
| 案例 | 遙測時間序列和警示。 例如，每隔 5 分鐘傳送一次的 256 KB 感應器資料批次。 | 可用的功能與條件。 例如，hello 目前裝置連線模式例如行動電話通訊或 Wi-fi。 同步處理長時間執行的工作流程，例如組態與軟體更新。 | 媒體檔案。 大型 (通常已壓縮的) 遙測批次。 |
| 儲存和擷取 | IoT 中樞來暫時儲存向上 too7 天。 僅限循序讀取。 | IoT 中樞存 hello 裝置兩個。 擷取使用 hello [IoT 中樞的查詢語言][lnk-query]。 | 儲存在使用者提供的 Azure 儲存體帳戶中。 |
| 大小 | Too256 KB 的訊息。 | 最大回報屬性大小為 8 KB。 | Azure Blob 儲存體所支援的檔案大小上限。 |
| 頻率 | 高。 如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。 | 中。 如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。 | 低。 如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。 |
| 通訊協定 | 適用於所有通訊協定。 | 目前僅適用於使用 MQTT 時。 | 當使用任何通訊協定，但需要 HTTP hello 裝置上才能使用。 |

可能的應用程式需要為遙測時間序列或警示，且 toomake tooboth 傳送資訊提供 hello 裝置兩個。 在此案例中，您可以選擇使用的下列選項的 hello:

* hello 裝置應用程式傳送裝置到雲端訊息，並報告屬性變更。
* hello 方案後端在收到 hello 訊息時，可以在 hello 裝置兩個的標記儲存 hello 資訊。

因為裝置到雲端訊息啟用更高輸送量比裝置兩個更新，可能會很理想 tooavoid 更新 hello 裝置兩個的每一個裝置到雲端訊息。


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
