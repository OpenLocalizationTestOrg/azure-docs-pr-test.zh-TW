---
title: "aaaUse 度量 toomonitor Azure IoT 中樞 |Microsoft 文件"
description: "如何 toouse Azure IoT 中樞度量 tooassess 和監視器 hello IoT 中樞的整體健全狀況。"
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>了解 IoT 中樞計量
IoT 中樞度量提供您更佳 hello Azure IoT 資源 hello 狀態相關的資料中您 Azure 訂用帳戶。 IoT 中樞度量啟用您 tooassess hello hello IoT 中心服務和 hello 裝置的整體健全狀況連接 tooit。 使用者互動的統計資料很重要的因為它們可以協助您查看如何運作的 IoT 中樞與說明根本原因問題而不需要 toocontact Azure 支援。

預設會啟用計量。 您可以檢視來自 hello Azure 入口網站的 IoT 中樞度量。

## <a name="how-tooview-iot-hub-metrics"></a>如何 tooview IoT 中樞度量
1. 建立 IoT 中樞。 您可以找到指示如何 toocreate hello IoT 中樞[開始][ lnk-get-started]指南。
2. 開啟您的 IoT 中樞的 hello 刀鋒視窗。 按一下此處的 [計量]。
   
    ![][1]
3. Hello 計量刀鋒視窗中，從您可以檢視您的 IoT 中樞 hello 度量，並建立自訂檢視的度量。 您可以按一下 選擇 toosend 度量資料 tooan 事件中樞端點或 Azure 儲存體帳戶**診斷設定**。
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>IoT 中樞度量以及如何 toouse 它們
IoT 中樞提供許多標準 toogive 您概觀中樞和 hello hello 健康狀態的總數連接的裝置。 您可以結合來自多個度量 toopaint 宏觀 hello hello IoT 中樞狀態的資訊。 hello 下表描述每個 IoT 中樞會將追蹤，hello 度量和狀態的方式每個度量與整體 toohello hello IoT 中樞。

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|遙測訊息傳送嘗試|Count|總計|送出的遙測裝置到雲端訊息嘗試 toobe 數目 tooyour IoT 中樞|
|d2c.telemetry.ingress.success|已傳送的遙測訊息|Count|總計|裝置到雲端遙測訊息數目已成功傳送 tooyour IoT 中樞|
|c2d.commands.egress.complete.success|完成的命令|Count|總計|雲端到裝置命令已順利完成 hello 裝置數目|
|c2d.commands.egress.abandon.success|放棄的命令|Count|總計|放棄 hello 裝置的雲端到裝置命令數目|
|c2d.commands.egress.reject.success|拒絕的命令|Count|總計|雲端到裝置 hello 裝置被拒絕的命令數目|
|devices.totalDevices|裝置總計|Count|總計|已登錄的裝置數 tooyour IoT 中樞|
|devices.connectedDevices.allProtocol|連接的裝置|Count|總計|連接的裝置數目 tooyour IoT 中樞|
|d2c.telemetry.egress.success|已傳遞的遙測訊息|Count|總計|訊息已成功地寫入 tooendpoints （總計） 的次數|
|d2c.telemetry.egress.dropped|捨棄的訊息|Count|總計|卸除的訊息數目，因為它們不符合任何路由 hello 後援路由已停用|
|d2c.telemetry.egress.orphaned|被遺棄的訊息|Count|總計|訊息不符合任何包括 hello 後援路由的路由的 hello 數目|
|d2c.telemetry.egress.invalid|無效的訊息|Count|總計|hello 的訊息計數不會傳遞到期 tooincompatibility 與 hello 端點|
|d2c.telemetry.egress.fallback|符合後援條件的訊息|Count|總計|寫入 toohello 後援端點的訊息數|
|d2c.endpoints.egress.eventHubs|訊息傳遞 tooEvent 中樞端點|Count|總計|訊息已成功寫入的 tooEvent 中心端點的次數|
|d2c.endpoints.latency.eventHubs|事件中樞端點的訊息延遲|毫秒|平均值|hello 之間的平均延遲訊息輸入 toohello IoT 中樞與訊息輸入至事件中心的端點，以毫秒為單位|
|d2c.endpoints.egress.serviceBusQueues|訊息傳遞 tooService 匯流排佇列端點|Count|總計|訊息已成功寫入的 tooService 匯流排佇列端點的次數|
|d2c.endpoints.latency.serviceBusQueues|服務匯流排佇列端點的訊息延遲|毫秒|平均值|hello 之間的平均延遲訊息輸入 toohello IoT 中樞與訊息輸入至服務匯流排佇列端點，以毫秒為單位|
|d2c.endpoints.egress.serviceBusTopics|訊息傳遞 tooService 匯流排主題端點|Count|總計|訊息已成功寫入的 tooService 匯流排主題端點的次數|
|d2c.endpoints.latency.serviceBusTopics|服務匯流排主題端點的訊息延遲|毫秒|平均值|hello 之間的平均延遲訊息輸入 toohello IoT 中樞與訊息輸入至服務匯流排主題端點，以毫秒為單位|
|d2c.endpoints.egress.builtIn.events|訊息傳遞 toohello 內建端點 （訊息/事件）|Count|總計|訊息已成功寫入的 toohello 內建端點 （訊息/事件） 的次數|
|d2c.endpoints.latency.builtIn.events|Hello 內建端點 （訊息/事件） 的訊息延遲|毫秒|平均值|hello 之間的平均延遲訊息輸入 toohello IoT 中樞與訊息輸入至 hello 內建端點 （訊息/事件），以毫秒為單位 |
|d2c.twin.read.success|裝置的成功對應項讀取|Count|總計|讀取所有成功的裝置啟動兩個 hello 計數。|
|d2c.twin.read.failure|裝置的失敗對應項讀取|Count|總計|所有的 hello 計數失敗裝置起始兩個讀取。|
|d2c.twin.read.size|裝置的對應項讀取回應大小|位元組|平均值|hello 平均、 最小值 和所有成功的最大裝置起始 twin 讀取。|
|d2c.twin.update.success|裝置的成功對應項更新|Count|總計|所有成功的裝置啟動兩個更新的 hello 計數。|
|d2c.twin.update.failure|裝置的失敗對應項更新|Count|總計|hello 計數的所有失敗的裝置啟動兩個更新。|
|d2c.twin.update.size|裝置的對應項更新大小|位元組|平均值|hello 平均、 最小值 和所有成功的最大大小裝置起始 twin 更新。|
|c2d.methods.success|成功直接方法叫用|Count|總計|所有成功的直接方法呼叫 hello 計數。|
|c2d.methods.failure|失敗直接方法叫用|Count|總計|所有的 hello 計數無法直接方法呼叫。|
|c2d.methods.requestSize|直接方法叫用的要求大小|位元組|平均值|hello 平均、 最小值 和所有成功的直接方法要求的最大值。|
|c2d.methods.responseSize|直接方法叫用的回應大小|位元組|平均值|hello 平均、 最小值 和所有成功的直接方法回應的最大值。|
|c2d.twin.read.success|後端的成功對應項讀取|Count|總計|讀取所有成功的後端初始化兩個 hello 計數。|
|c2d.twin.read.failure|後端的失敗對應項讀取|Count|總計|所有的 hello 計數失敗後結束起始兩個讀取。|
|c2d.twin.read.size|後端的對應項讀取回應大小|位元組|平均值|hello 平均、 最小值和最大值的所有成功後結束起始 twin 讀取。|
|c2d.twin.update.success|後端的成功對應項更新|Count|總計|所有成功的後端初始化兩個更新的 hello 計數。|
|c2d.twin.update.failure|後端的失敗對應項更新|Count|總計|所有的 hello 計數失敗後結束起始兩個更新。|
|c2d.twin.update.size|後端的對應項更新大小|位元組|平均值|hello 平均、 最小值 和所有成功的最大大小後結束起始 twin 更新。|
|twinQueries.success|成功對應項查詢|Count|總計|所有成功的兩個查詢的 hello 計數。|
|twinQueries.failure|失敗對應項查詢|Count|總計|所有失敗的兩個查詢的 hello 計數。|
|twinQueries.resultSize|對應項查詢結果大小|位元組|平均值|hello 平均、 最小值、 和 hello 所有成功的兩個查詢的結果大小的最大值。|
|jobs.createTwinUpdateJob.success|成功建立的對應項更新作業|Count|總計|hello 所有成功建立兩個更新作業數目。|
|jobs.createTwinUpdateJob.failure|建立失敗的對應項更新作業|Count|總計|建立兩個更新作業的所有失敗的 hello 計數。|
|jobs.createDirectMethodJob.success|成功建立的方法叫用作業|Count|總計|hello 所有成功建立直接的方法引動過程作業數目。|
|jobs.createDirectMethodJob.failure|建立失敗的方法叫用作業|Count|總計|建立直接的方法引動過程作業的所有失敗的 hello 計數。|
|jobs.listJobs.success|成功呼叫 toolist 工作|Count|總計|所有成功呼叫 toolist 作業 hello 計數。|
|jobs.listJobs.failure|失敗的呼叫 toolist 工作|Count|總計|所有的失敗的呼叫 toolist 作業 hello 計數。|
|jobs.cancelJob.success|成功取消作業|Count|總計|所有成功的 hello 計數呼叫 toocancel 作業。|
|jobs.cancelJob.failure|取消作業失敗|Count|總計|所有失敗的呼叫 toocancel 作業 hello 計數。|
|jobs.queryJobs.success|成功作業查詢|Count|總計|所有成功呼叫 tooquery 作業 hello 計數。|
|jobs.queryJobs.failure|失敗作業查詢|Count|總計|所有的失敗的呼叫 tooquery 作業 hello 計數。|
|jobs.completed|已完成的工作|Count|總計|hello 與所有已完成的工作數目。|
|jobs.failed|失敗作業|Count|總計|hello 所有失敗的作業數目。|

## <a name="next-steps"></a>後續步驟
既然您已看過的 IoT 中樞度量概觀，請依照此連結 toolearn 更多關於管理 Azure IoT 中樞：

* [作業監視][lnk-monitor]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
