---
title: "aaaUnderstand Azure IoT 中樞作業 |Microsoft 文件"
description: "開發人員指南-排定多個裝置上的作業 toorun 連接 tooyour IoT 中樞。 作業可以在多個裝置上更新標籤和所需的屬性，並叫用直接方法。"
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
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>排程多個裝置上的作業
## <a name="overview"></a>概觀
如前面幾篇文章所述，Azure IoT 中樞可啟用許多建置組塊 ([裝置對應項屬性和標籤][lnk-twin-devguide]和[直接方法][lnk-dev-methods])。  一般而言後, 端應用程式啟用裝置系統管理員和操作員 tooupdate 並與其互動 IoT 裝置之間能夠大量並在排定的時間。  工作會封裝在排程時間的 hello 執行裝置的兩個更新和直接的方法，針對一組裝置。  例如，操作員會使用後端應用程式會起始與追蹤工作 tooreboot 一組裝置不會干擾 toohello hello 建置作業一次建置 43 和樓層 3。

### <a name="when-toouse"></a>當 toouse
請考慮使用工作的時機： 方案後端需要 tooschedule 和追蹤進度任何 hello 一組裝置的下列活動：

* 更新所需屬性
* 更新標籤
* 叫用直接方法

## <a name="job-lifecycle"></a>作業生命週期
作業會由 hello 方案後端所起始和維護的 IoT 中樞。  您可以透過面向服務的 URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) 起始作業，並透過面向服務的 URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`) 查詢執行中作業的進度。  一次作業會起始，查詢作業啟用 hello 後端應用程式 toorefresh hello 狀態執行的作業。

> [!NOTE]
> 當您起始的作業時，屬性名稱和值只能包含 US-ASCII 可列印英數字元、 在 hello 下列設定除外： ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``。
> 
> 

## <a name="reference-topics"></a>參考主題：
hello 下列參考主題提供有關使用 工作詳細資訊。

## <a name="jobs-tooexecute-direct-methods"></a>作業 tooexecute 直接方法
hello 如下 hello HTTP 1.1 要求詳細資料，執行[直接方法][ lnk-dev-methods]一組使用作業的裝置上：

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
hello 查詢條件也可以是單一裝置識別碼或裝置識別碼的清單如下所示

**範例**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[IoT 中樞查詢語言][lnk-query]涵蓋了IoT 中樞查詢語言的其他詳細資料。

## <a name="jobs-tooupdate-device-twin-properties"></a>作業 tooupdate 裝置兩個屬性
hello 下面是 hello HTTP 1.1 要求詳細資料，更新裝置使用作業的兩個屬性：

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
hello 如下 hello HTTP 1.1 要求詳細資料，如[查詢作業][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

hello continuationToken hello 回應中提供。  

## <a name="jobs-properties"></a>作業屬性
hello 下列是屬性對應的描述，可用於查詢時的工作或作業結果的清單。

| 屬性 | 說明 |
| --- | --- |
| **jobId** |應用程式提供 hello 作業識別碼。 |
| **startTime** |應用程式提供 hello 工作的開始時間 (ISO 8601)。 |
| **endTime** |IoT 中樞 hello 作業完成時的日期 (ISO 8601) 提供。 Hello 作業到達完成' hello 狀態之後，才有效。 |
| **type** |作業類型： |
| **scheduledUpdateTwin**: 作業，以便用 tooupdate 一組所需的屬性或標記。 | |
| **scheduledDeviceMethod**: 作業，以便用 tooinvoke 裝置上的方法裝置雙一組。 | |
| **狀態** |Hello 作業的目前狀態。 狀態的可能值︰ |
| **暫止**： 排程並等候 toobe 收取 hello 工作服務。 | |
| **排程**： 排程在未來的 hello 的時間。 | |
| **執行中**︰目前作用中的作業。 | |
| **取消**︰作業已遭到取消。 | |
| **失敗**︰作業失敗。 | |
| **完成**︰作業完成。 | |
| **deviceJobStatistics** |Hello 作業的執行統計資料。 |

**deviceJobStatistics** 屬性。

| 屬性 | 說明 |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Hello 作業中的裝置數目。 |
| **deviceJobStatistics.failedCount** |Hello 作業失敗的裝置數目。 |
| **deviceJobStatistics.succeededCount** |Hello 作業成功，其中的裝置數目。 |
| **deviceJobStatistics.runningCount** |目前正在 hello 工作的裝置數目。 |
| **deviceJobStatistics.pendingCount** |Toorun hello 作業擱置的裝置數目。 |

### <a name="additional-reference-material"></a>其他參考資料
Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：

* [IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。
* [節流和配額][ lnk-quotas]描述 hello 配額套用 toohello IoT 中心服務和 hello 節流行為 tooexpect，當您使用 hello 服務。
* [Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言的 Sdk 可以與 IoT 中樞開發裝置與服務互動的應用程式時使用。
* [IoT 中樞裝置雙、 作業和訊息路由的查詢語言][ lnk-query]描述 hello IoT 中樞的查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。
* [IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。

## <a name="next-steps"></a>後續步驟
如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程中的 hello:

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
