---
title: "了解 Azure IoT 中樞作業 | Microsoft Docs"
description: "開發人員指南 - 排定在連接至 IoT 中樞的多個裝置上執行作業。 作業可以在多個裝置上更新標籤和所需的屬性，並叫用直接方法。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>排程多個裝置上的作業
## <a name="overview"></a>概觀
如前面幾篇文章所述，Azure IoT 中樞可啟用許多建置組塊 ([裝置對應項屬性和標籤][lnk-twin-devguide]和[直接方法][lnk-dev-methods])。  一般而言，後端應用程式可讓裝置管理員和操作員在排定的時間大量更新 IoT 裝置並與之互動。  作業可將在排定時間針對一組裝置執行裝置對應項更新和直接方法的操作封裝起來。  例如，操作員會使用後端應用程式來起始和追蹤作業，在不干擾大樓運作的時段，將 43 號大樓 3 樓的一組裝置重新開機。

### <a name="when-to-use"></a>使用時機
當解決方案後端需要排程和追蹤一組裝置的下列任何活動進度時，請考慮使用作業︰

* 更新所需屬性
* 更新標籤
* 叫用直接方法

## <a name="job-lifecycle"></a>作業生命週期
作業由解決方案後端起始，並由 IoT 中樞維護。  您可以透過面向服務的 URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) 起始作業，並透過面向服務的 URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`) 查詢執行中作業的進度。  作業起始後，只要查詢作業，就可讓後端應用程式重新整理執行中作業的狀態。

> [!NOTE]
> 當您起始作業時，屬性名稱和值只能包含 US-ASCII 可列印英數字元，下列集合中的任何字元除外︰``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``。
> 
> 

## <a name="reference-topics"></a>參考主題：
下列參考主題會提供您關於使用作業的詳細資訊。

## <a name="jobs-to-execute-direct-methods"></a>用以執行直接方法的作業
以下是使用作業在一組裝置上執行[直接方法][lnk-dev-methods]的 HTTP 1.1 要求詳細資料︰

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
查詢條件也可以在單一裝置識別碼或裝置識別碼清單中，如下所示

**範例**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[IoT 中樞查詢語言][lnk-query]涵蓋了IoT 中樞查詢語言的其他詳細資料。

## <a name="jobs-to-update-device-twin-properties"></a>用以更新裝置對應項屬性的作業
以下是使用作業更新裝置對應項屬性的 HTTP 1.1 要求詳細資料︰

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>查詢作業的進度
以下是用於[查詢作業][lnk-query]的 HTTP 1.1 要求詳細資料：

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

ContinuationToken 會從回應來提供。  

## <a name="jobs-properties"></a>作業屬性
以下是屬性和相對應說明的清單，可於查詢作業或作業結果時使用。

| 屬性 | 說明 |
| --- | --- |
| **jobId** |應用程式所提供的作業識別碼。 |
| **startTime** |應用程式所提供的作業開始時間 (ISO-8601)。 |
| **endTime** |IoT 中樞所提供的作業完成日期 (ISO-8601)。 在作業到達「已完成」狀態後才有效。 |
| **type** |作業類型： |
| **scheduledUpdateTwin**︰用來更新一組所需屬性或標籤的作業。 | |
| **scheduledDeviceMethod**︰用來在一組裝置對應項上叫用裝置方法的作業。 | |
| **狀態** |作業的目前狀態。 狀態的可能值︰ |
| **擱置中**︰已排定並等候作業服務揀選。 | |
| **已排程**︰已排定未來時間。 | |
| **執行中**︰目前作用中的作業。 | |
| **取消**︰作業已遭到取消。 | |
| **失敗**︰作業失敗。 | |
| **完成**︰作業完成。 | |
| **deviceJobStatistics** |作業執行的相關統計資料。 |

**deviceJobStatistics** 屬性。

| 屬性 | 說明 |
| --- | --- |
| **deviceJobStatistics.deviceCount** |作業中的裝置數目。 |
| **deviceJobStatistics.failedCount** |作業失敗的裝置數目。 |
| **deviceJobStatistics.succeededCount** |作業成功的裝置數目。 |
| **deviceJobStatistics.runningCount** |目前正在執行作業的裝置數目。 |
| **deviceJobStatistics.pendingCount** |等待執行作業的裝置數目。 |

### <a name="additional-reference-material"></a>其他參考資料
IoT 中樞開發人員指南中的其他參考主題包括︰

* [IoT 中樞端點][lnk-endpoints]說明每個 IoT 中樞公開給執行階段和管理作業的各種端點。
* [節流和配額][lnk-quotas]說明適用於 IoT 中樞服務的配額，和使用服務時所預期的節流行為。
* [Azure IoT 中樞裝置和服務 SDK][lnk-sdks] 列出各種語言 SDK，讓您在開發可與 IoT 中樞互動的裝置和服務應用程式時使用。
* [裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-query]說明可用於從 IoT 中樞擷取有關裝置對應項和作業資訊的 IoT 中樞查詢語言。
* [IoT 中樞 MQTT 支援][lnk-devguide-mqtt]針對 MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。

## <a name="next-steps"></a>後續步驟
如果您想要嘗試本文章所述的概念，您可能會對下列 IoT 中樞教學課程感興趣：

* [排程及廣播作業][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
