---
title: "Azure IoT 中樞 aaaUnderstand 直接方法 |Microsoft 文件"
description: "開發人員指南-使用直接的方法 tooinvoke 程式碼，在您的服務應用程式的裝置上。"
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>了解 IoT 中樞的直接方法並從中樞叫用直接方法
## <a name="overview"></a>概觀
IoT 中樞讓您能夠 tooinvoke 直接的方法在 hello 雲端的裝置上。 直接方法代表與裝置的類似 tooan，在於它們成功或失敗 （之後立即使用者指定的逾時），呼叫 HTTP 要求-回覆之間的互動。 這是適合的情況下立即採取行動的 hello 課程 hello 裝置是否可以 toorespond，例如傳送 SMS 喚醒 tooa 裝置，如果裝置已離線 (SMS 正在成本高於方法呼叫) 而有所不同。

每個裝置方法的目標是單一裝置。 [作業][ lnk-devguide-jobs]提供多個裝置，方式 tooinvoke 直接的方法，並排定方法引動過程已中斷連線的裝置。

IoT 中樞上具有**服務連線**權限的任何人都可以叫用裝置上的方法。

### <a name="when-toouse"></a>當 toouse
直接的方法會遵循要求-回應模式，而需要立即確認其結果，通常是互動式控制權，hello 裝置，例如 tooturn 上 風扇的通訊開放。

請參閱太[雲端到裝置通訊指引][ lnk-c2d-guidance]使用所需的屬性之間的不確定，直接方法或雲端到裝置訊息。

## <a name="method-lifecycle"></a>方法生命週期
直接的方法會實作 hello 裝置上，而且可能需要零或多個輸入 hello 方法裝載 toocorrectly 中的具現化。 您可以透過面向服務的 URI 叫用直接方法 (`{iot hub}/twins/{device id}/methods/`)。 裝置會透過裝置特定 MQTT 主題收到直接方法 (`$iothub/methods/POST/{method name}/`)。 我們可能支援其他的裝置後端網路通訊協定，在未來的 hello 直接的方法。

> [!NOTE]
> 當您叫用的裝置上直接方法時，屬性名稱和值只能包含 US-ASCII 可列印英數字元、 在 hello 下列設定除外： ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``。
> 
> 

直接方法是同步，可能會成功或失敗之後 hello 逾時期限 (預設： 30 秒，可設定總 too3600 秒)。 直接的方法可用於互動式案例中，您的裝置 tooact 才 hello 裝置是線上和接收的命令，例如開啟的燈號電話。 在這些情況下，您想 toosee 立即成功或失敗所以 hello 雲端服務可以儘速處理 hello 結果。 hello 裝置可能會傳回 hello 方法，因為某些訊息本文，但不需要 hello 方法 toodo 如此。 不保證方法呼叫的順序或任何並行語意。

直接的方法是僅限 HTTP 從 hello 雲端端，和 MQTT 僅從 hello 裝置端。

方法要求和回應的 hello 裝載是總 too8KB JSON 文件。

## <a name="reference-topics"></a>參考主題：
hello 下列參考主題提供有關使用直接的方法的詳細資訊。

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>從後端應用程式叫用直接方法
### <a name="method-invocation"></a>方法引動過程
裝置上的直接方法引動過程是 HTTP 呼叫，包含︰

* hello *URI*特定 toohello 裝置 (`{iot hub}/twins/{device id}/methods/`)
* hello POST*方法*
* *標頭*其中包含 hello 的授權，請要求識別碼、 內容類型和內容編碼方式
* 透明 JSON*主體*在 hello 下列格式：

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

逾時 (秒)。 如果未設定逾時，它會預設 too30 秒。

### <a name="response"></a>Response
hello 後端應用程式收到的回應所組成：

* *HTTP 狀態碼*，用來自 hello IoT 中樞的錯誤，包括 404 錯誤的裝置目前未連接
* *標頭*其中包含 hello ETag，要求識別碼、 內容類型和內容編碼方式
* JSON*主體*在 hello 下列格式：

```
{
    "status" : 201,
    "payload" : {...}
}
```

   同時`status`和`body`hello 裝置所提供，且 toorespond 搭配 hello 裝置本身的狀態碼和/或描述。

## <a name="handle-a-direct-method-on-a-device"></a>在裝置上處理直接方法
### <a name="method-invocation"></a>方法引動過程
裝置收到 hello MQTT 主題上的直接方法要求：`$iothub/methods/POST/{method name}/?$rid={request id}`

哪些 hello 裝置收到 hello 主體為下列格式的 hello:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

方法要求為 QoS 0。

### <a name="response"></a>Response
hello 裝置所傳送的回應太`$iothub/methods/res/{status}/?$rid={request id}`，其中：

* hello`status`屬性是 hello 方法執行的裝置提供狀態。
* hello`$rid`屬性是從 IoT 中樞從收到 hello 方法引動過程的 hello 要求識別碼。

hello 主體由 hello 裝置設定，而且可以是任何狀態。

## <a name="additional-reference-material"></a>其他參考資料
Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：

* [IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。
* [節流和配額][ lnk-quotas]描述 hello 配額套用 toohello IoT 中心服務和 hello 節流行為 tooexpect，當您使用 hello 服務。
* [Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用的 Sdk。
* [IoT 中樞裝置雙、 作業和訊息路由的查詢語言][ lnk-query]描述 hello IoT 中樞的查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。
* [IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。

## <a name="next-steps"></a>後續步驟
現在您已經學會如何 toouse 直接的方法，您可能會想要 hello 遵循 IoT 中樞開發人員指南 》 主題：

* [排程多個裝置上的作業][lnk-devguide-jobs]

如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程中的 hello:

* [使用直接方法][lnk-methods-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
