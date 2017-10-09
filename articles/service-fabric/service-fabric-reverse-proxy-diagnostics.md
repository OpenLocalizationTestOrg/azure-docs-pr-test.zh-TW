---
title: "Service Fabric aaaAzure 反向 proxy 診斷 |Microsoft 文件"
description: "深入了解如何 toomonitor 並診斷在 hello 反向 proxy 的要求處理。"
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>監視，並診斷在 hello 反向 proxy 的要求處理

從 Service Fabric 的 hello 5.7 版開始，反向 proxy 事件可用於集合。 hello 事件可用於在兩個通道，一個只有錯誤事件的相關 toorequest hello 反向 proxy 和包含成功和失敗要求的項目的詳細資料事件的第二個通道的處理失敗。

請參閱太[收集反向 proxy 事件](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events)tooenable 從這些通道本機和 Azure Service Fabric 叢集收集事件。

## <a name="troubleshoot-using-diagnostics-logs"></a>使用診斷記錄進行疑難排解
以下是上如何 toointerpret hello 常見失敗記錄檔的其中可能會遇到的一些範例：

1. 反向 proxy 傳回回應狀態碼 504 (逾時)。

    其中一個原因可能由於 toohello 服務失敗 tooreply hello 要求逾時期限內。
hello 以下的第一個事件記錄 hello hello 反向 proxy 在收到 hello 要求詳細資料。 hello 第二個事件表示該 hello 要求失敗時轉送 tooservice 由於太 「 內部錯誤 = ERROR_WINHTTP_TIMEOUT" 

    hello 裝載包含：

    *  **traceId**： 這個 GUID 可使用 toocorrelate 對應 tooa 單一要求的所有 hello 事件。 在以下兩個事件的 hello，hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**，意味著所屬 toohello 相同的要求。
    *  **requestUrl**: hello 的 URL (反向 proxy URL) toowhich hello 要求已傳送。
    *  **指令動詞**︰HTTP 指令動詞。
    *  **remoteAddress**： 傳送嗨要求的用戶端的位址。
    *  **resolvedServiceUrl**： 解決服務端點 URL toowhich hello 連入要求的時間。 
    *  **errorDetails**: hello 失敗的其他資訊。

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. 反向 proxy 傳回回應狀態碼 404 (找不到)。 
    
    以下是範例事件反向 proxy 位置傳回 404，因為它無法 toofind hello 比對服務端點。
    重要的 hello 裝載項目為：
    *  **processRequestPhase**： 指出在 hello 失敗發生時，處理要求期間 hello 階段***TryGetEndpoint***也就是 同時嘗試 toofetch hello 服務端點 tooforward 至。 
    *  **errorDetails**： 列出 hello 端點搜尋準則。 您可以在此處查看指定該 hello listenerName = **FrontEndListener** hello 複本端點清單只包含名稱為 hello 接聽程式而**OldListener**。
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    另一個範例，其中反向 proxy 可能會傳回 404 找不到為： ApplicationGateway\Http 組態參數**SecureOnlyMode**設定 hello 反向 proxy 接聽 tootrue **HTTPS**，不過，所有 hello 複本端點都不安全 （接聽 HTTP）。
    因為找不到端點接聽 HTTPS tooforward hello 要求反向 proxy 傳回 404。 分析 hello 事件裝載中的 hello 參數，可協助 toonarrow 向 hello 問題：
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. 要求 toohello 反向 proxy 逾時錯誤而失敗。 
    hello 事件記錄檔會包含一個事件 （此處未顯示） 收到 hello 要求詳細資料。
    hello 下一個事件會顯示 hello 服務回應 404 狀態碼，並反向 proxy 可讓您起始重新解析。 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    當收集 hello 的所有事件，您會看到火車的每個解決和正嘗試顯示的事件。
    hello hello 數列中的最後一個事件會顯示 hello 要求處理失敗，發生逾時，以及 hello 成功解決嘗試的次數。
    
    > [!NOTE]
    > 它建議的預設停用 tookeep hello verbose 通道事件集合，並啟用供疑難排解以需求為基礎。

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    如果集合已啟用只適用於重大/錯誤事件，您會看到一個事件 hello 逾時和 hello 次數解析的相關詳細資料。 
    
    如果 hello 服務想 toosend 404 狀態程式碼後 toohello 使用者，它應該伴隨 「 X ServiceFabric"標頭。 修正此問題之後，您會看到該反向 proxy 轉送 hello 狀態程式碼後 toohello 用戶端。  

4. Hello 用戶端已中斷連線的情況下 hello 要求。

    反向 proxy 轉送 hello 回應 tooclient 但 hello 用戶端中斷連接時，會記錄下列事件 hello:

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> 目前不記錄事件相關的 toowebsocket 要求處理。 這將會加入 hello 下一個版本中。

## <a name="next-steps"></a>後續步驟
* [使用 Windows Azure 診斷的事件彙總和收集](service-fabric-diagnostics-event-aggregation-wad.md)，以便在 Azure 叢集中啟用記錄收集。
* tooview Service Fabric 事件，在 Visual Studio 中，請參閱[監視及診斷在本機](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。
* 請參閱太[設定反向 proxy tooconnect toosecure 服務](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services)Azure 資源管理員的範本範例 tooconfigure 安全反向 proxy hello 不同的服務憑證驗證選項。
* 讀取[Service Fabric 反向 proxy](service-fabric-reverseproxy.md) toolearn 更多。
