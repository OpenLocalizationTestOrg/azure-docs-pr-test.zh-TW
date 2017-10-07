---
title: "IoT 中樞雲端到裝置 aaaAzure 選項 |Microsoft 文件"
description: "開發人員指南-指引 toouse 時直接的方法、 兩個裝置所需的屬性或雲端到裝置訊息雲端到裝置通訊。"
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Cloud-to-device communications guidance
IoT 中心提供裝置應用程式 tooexpose 功能 tooa 後端應用程式的三個的選項：

* [直接方法][ lnk-methods]需要立即確認 hello 結果的通訊。 直接方法通常用於裝置的互動式控制，例如開啟風扇。
* [兩個的所需屬性][ lnk-twins]的長時間執行的命令可讓您能 tooput hello 裝置插入特定預期狀態。 例如，設定 hello 遙測傳送間隔 too30 分鐘數。
* [雲端到裝置訊息][ lnk-c2d]單向通知 toohello 裝置應用程式。

以下是 hello 的詳細的比較雲端到裝置通訊的各種選項。

|  | 直接方法 | 對應項的所需屬性 | 雲端到裝置的訊息 |
| ---- | ------- | ---------- | ---- |
| 案例 | 需要立即確認的命令，例如開啟風扇。 | 長時間執行的命令適 tooput hello 裝置特定的所需的狀態。 例如，設定 hello 遙測傳送間隔 too30 分鐘數。 | 單向通知 toohello 裝置應用程式。 |
| 資料流 | 雙向。 hello 裝置應用程式可以立即回應 toohello 方法。 hello 方案後端收到 hello 結果客 toohello 要求。 | 單向。 hello 裝置應用程式會收到一則通知 hello 屬性變更。 | 單向。 hello 裝置應用程式收到 hello 訊息
| 耐久性 | 無法聯繫已中斷連接的裝置。 hello 方案後端會收到該 hello 裝置未連接。 | 屬性值會保留在 hello 裝置兩個。 裝置會在下一次重新連線時讀取它。 屬性值會以 hello 可擷取[IoT 中樞的查詢語言][lnk-query]。 | IoT 中樞可以保留訊息 too48 時數。 |
| 目標 | 使用 **deviceId** 的單一裝置，或使用[作業][lnk-jobs]的多個裝置。 | 使用 **deviceId** 的單一裝置，或使用[作業][lnk-jobs]的多個裝置。 | 依照 **deviceId** 的單一裝置。 |
| 大小 | 向上 too8KB 要求和 8 KB 的回應。 | 所需屬性大小上限為 8KB。 | Too64KB 訊息。 |
| 頻率 | 高。 如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。 | 中。 如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。 | 低。 如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。 |
| 通訊協定 | 目前僅適用於使用 MQTT 時。 | 目前僅適用於使用 MQTT 時。 | 適用於所有通訊協定。 裝置必須在使用 HTTP 時進行輪詢。 |

了解 toouse 如何直接的方法、 所需的屬性和雲端到裝置訊息 hello 遵循教學課程中：

* [使用直接方法][lnk-methods-tutorial]，適用於直接方法；
* [使用所需的屬性 tooconfigure 裝置][lnk-twin-properties]，針對裝置的兩個的預期屬性。 
* [傳送雲端到裝置訊息][lnk-c2d-tutorial]，適用於雲端到裝置訊息。

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
