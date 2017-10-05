---
title: "Azure Service Fabric 反向 Proxy 診斷 | Microsoft Docs"
description: "了解如何在反向 proxy 監視和診斷要求處理。"
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
ms.openlocfilehash: 3bc631606afbc93d5bca94f4955fd2ef816fa9fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-request-processing-at-the-reverse-proxy"></a><span data-ttu-id="40225-103">在反向 proxy 監視和診斷要求處理</span><span class="sxs-lookup"><span data-stu-id="40225-103">Monitor and diagnose request processing at the reverse proxy</span></span>

<span data-ttu-id="40225-104">從 Service Fabric 5.7 版開始，反向 proxy 事件可供收集。</span><span class="sxs-lookup"><span data-stu-id="40225-104">Starting with the 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="40225-105">事件可用於兩個通道，第一個通道只有在反向 proxy 的要求處理失敗相關錯誤事件，而第二個通道包含成功和失敗要求項目的詳細資訊事件。</span><span class="sxs-lookup"><span data-stu-id="40225-105">The events are available in two channels, one with only error events related to request processing failure at the reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="40225-106">請參閱[收集反向 proxy 事件](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events)，允許從這些通道收集本機和 Azure Service Fabric 叢集中的事件。</span><span class="sxs-lookup"><span data-stu-id="40225-106">Refer to [Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) to enable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="40225-107">使用診斷記錄進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="40225-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="40225-108">下列範例有關如何解釋可能看見的常見失敗記錄：</span><span class="sxs-lookup"><span data-stu-id="40225-108">Here are some examples on how to interpret the common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="40225-109">反向 proxy 傳回回應狀態碼 504 (逾時)。</span><span class="sxs-lookup"><span data-stu-id="40225-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="40225-110">其中一個原因可能是因為服務無法在要求逾時期間內回覆。</span><span class="sxs-lookup"><span data-stu-id="40225-110">One reason could be due to the service failing to reply within the request timeout period.</span></span>
<span data-ttu-id="40225-111">下面第一個事件記錄在反向 proxy 收到的要求詳細資料。</span><span class="sxs-lookup"><span data-stu-id="40225-111">The first event below logs the details of the request received at the reverse proxy.</span></span> <span data-ttu-id="40225-112">第二個事件指出要求在轉寄至服務時失敗，因為「內部錯誤 = ERROR_WINHTTP_TIMEOUT」</span><span class="sxs-lookup"><span data-stu-id="40225-112">The second event indicates that the request failed while forwarding to service, due to "internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="40225-113">承載包括︰</span><span class="sxs-lookup"><span data-stu-id="40225-113">The payload includes:</span></span>

    *  <span data-ttu-id="40225-114">**traceId**：此 GUID 可以讓對應至單一要求的所有事件相互關聯。</span><span class="sxs-lookup"><span data-stu-id="40225-114">**traceId**: This GUID can be used to correlate all the events corresponding to a single request.</span></span> <span data-ttu-id="40225-115">在以下兩個事件中，traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**，意味著它們屬於相同的要求。</span><span class="sxs-lookup"><span data-stu-id="40225-115">In the below two events, the traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong to the same request.</span></span>
    *  <span data-ttu-id="40225-116">**requestUrl**：要求所要送往的 URL (反向 proxy URL)。</span><span class="sxs-lookup"><span data-stu-id="40225-116">**requestUrl**: The URL (Reverse proxy URL) to which the request was sent.</span></span>
    *  <span data-ttu-id="40225-117">**指令動詞**︰HTTP 指令動詞。</span><span class="sxs-lookup"><span data-stu-id="40225-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="40225-118">**remoteAddress**：傳送要求之用戶端的位址。</span><span class="sxs-lookup"><span data-stu-id="40225-118">**remoteAddress**: Address of client sending the request.</span></span>
    *  <span data-ttu-id="40225-119">**resolvedServiceUrl**：傳入要求解析至的服務端點 URL。</span><span class="sxs-lookup"><span data-stu-id="40225-119">**resolvedServiceUrl**: Service endpoint URL to which the incoming request was resolved.</span></span> 
    *  <span data-ttu-id="40225-120">**errorDetails**︰關於失敗的額外資訊。</span><span class="sxs-lookup"><span data-stu-id="40225-120">**errorDetails**: Additional information about the failure.</span></span>

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
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request to service: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
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

2. <span data-ttu-id="40225-121">反向 proxy 傳回回應狀態碼 404 (找不到)。</span><span class="sxs-lookup"><span data-stu-id="40225-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="40225-122">在以下範例事件中，反向 proxy 傳回 404，因為它找不到相符的服務端點。</span><span class="sxs-lookup"><span data-stu-id="40225-122">Here is an example event where reverse proxy returns 404 since it failed to find the matching service endpoint.</span></span>
    <span data-ttu-id="40225-123">重要承載項目如下：</span><span class="sxs-lookup"><span data-stu-id="40225-123">The payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="40225-124">**processRequestPhase**：指出發生失敗時的要求處理期間階段，***TryGetEndpoint*** 也就是</span><span class="sxs-lookup"><span data-stu-id="40225-124">**processRequestPhase**: Indicates the phase during request processing when the failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="40225-125">嘗試提取要轉送至的服務端點時。</span><span class="sxs-lookup"><span data-stu-id="40225-125">while trying to fetch the service endpoint to forward to.</span></span> 
    *  <span data-ttu-id="40225-126">**errorDetails**：列出端點搜尋準則。</span><span class="sxs-lookup"><span data-stu-id="40225-126">**errorDetails**: Lists the endpoint search criteria.</span></span> <span data-ttu-id="40225-127">您可以查看指定的 listenerName = **FrontEndListener**，然而複本端點清單只包含名稱為 **OldListener** 的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="40225-127">Here you can see that the listenerName specified = **FrontEndListener** whereas the replica endpoint list only contains a listener with the name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward to service: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
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
    <span data-ttu-id="40225-128">反向 proxy 可能傳回 404 找不到的另一個範例為：ApplicationGateway\Http 組態參數 **SecureOnlyMode** 設為 true，且反向 proxy 在**HTTPS** 接聽，不過所有複本端點都不安全 (在 HTTP 上接聽)。</span><span class="sxs-lookup"><span data-stu-id="40225-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set to true with the reverse proxy listening on **HTTPS**, however all of the replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="40225-129">反向 proxy 傳回 404，因為它找不到在 HTTPS 上接聽的端點以轉送要求。</span><span class="sxs-lookup"><span data-stu-id="40225-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS to forward the request.</span></span> <span data-ttu-id="40225-130">在事件承載中分析參數有助於縮小問題範圍：</span><span class="sxs-lookup"><span data-stu-id="40225-130">Analyzing the parameters in the event payload helps to narrow down the issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="40225-131">反向 proxy 的要求因為逾時錯誤而失敗。</span><span class="sxs-lookup"><span data-stu-id="40225-131">Request to the reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="40225-132">事件記錄包含具有已接收要求詳細資料 (未顯示於此處) 的事件。</span><span class="sxs-lookup"><span data-stu-id="40225-132">The event logs contain an event with the received request details (not shown here).</span></span>
    <span data-ttu-id="40225-133">下一個事件顯示服務以 404 狀態碼回應，且反向 proxy 會起始重新解析。</span><span class="sxs-lookup"><span data-stu-id="40225-133">The next event shows that the service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request to service returned: status code = 404, status description = , Reresolving ",
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
    <span data-ttu-id="40225-134">收集所有事件時，您會看到一系列顯示每個解析和轉送嘗試的事件。</span><span class="sxs-lookup"><span data-stu-id="40225-134">When collecting all the events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="40225-135">序列中的最後一個事件顯示要求處理因為逾時而失敗，以及成功的解析嘗試次數。</span><span class="sxs-lookup"><span data-stu-id="40225-135">The last event in the series shows the request processing has failed with a timeout, along with the number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="40225-136">建議依預設停用詳細資訊通道事件收集功能，而後根據需求加以啟用以便進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="40225-136">It is recommended to keep the  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

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
    
    <span data-ttu-id="40225-137">如果只針對重大/錯誤事件啟用收集功能，您會看到一個包含逾時相關詳細資料和解析嘗試次數的事件。</span><span class="sxs-lookup"><span data-stu-id="40225-137">If collection is enabled for critical/error events only, you see one event with details about the timeout and the number of resolve attempts.</span></span> 
    
    <span data-ttu-id="40225-138">如果服務有意將 404 狀態碼傳回給使用者，應隨附 "X-ServiceFabric" 標頭。</span><span class="sxs-lookup"><span data-stu-id="40225-138">If the service intends to send a 404 status code back to the user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="40225-139">修正此問題後，您會看到反向 proxy 會將狀態碼轉送回用戶端。</span><span class="sxs-lookup"><span data-stu-id="40225-139">After fixing this, you will see that reverse proxy forwards the status code back to the client.</span></span>  

4. <span data-ttu-id="40225-140">用戶端已中斷要求連線的情況。</span><span class="sxs-lookup"><span data-stu-id="40225-140">Cases when the client has disconnected the request.</span></span>

    <span data-ttu-id="40225-141">當反向 proxy 將回應轉送至用戶端，但用戶端中斷連線時，就會記錄下列事件：</span><span class="sxs-lookup"><span data-stu-id="40225-141">The below event is recorded when reverse proxy is forwarding the response to client but the client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable to send response to client: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
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
> <span data-ttu-id="40225-142">目前不記錄 Websocket 要求處理的相關事件。</span><span class="sxs-lookup"><span data-stu-id="40225-142">Events related to websocket request processing are not currently logged.</span></span> <span data-ttu-id="40225-143">這將在下一版中新增。</span><span class="sxs-lookup"><span data-stu-id="40225-143">This will be added in the next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40225-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="40225-144">Next steps</span></span>
* <span data-ttu-id="40225-145">[使用 Windows Azure 診斷的事件彙總和收集](service-fabric-diagnostics-event-aggregation-wad.md)，以便在 Azure 叢集中啟用記錄收集。</span><span class="sxs-lookup"><span data-stu-id="40225-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="40225-146">若要在 Visual Studio 中檢視 Service Fabric 事件，請參閱[在本機上監視及診斷](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。</span><span class="sxs-lookup"><span data-stu-id="40225-146">To view Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="40225-147">如需 Azure Resource Manager 範本範例，以便使用不同的服務憑證驗證選項來設定安全反向 Proxy，請參閱[設定反向 Proxy 以連接安全的服務](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services)。</span><span class="sxs-lookup"><span data-stu-id="40225-147">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="40225-148">如需詳細資訊，請讀取 [Service Fabric 反向 proxy](service-fabric-reverseproxy.md)。</span><span class="sxs-lookup"><span data-stu-id="40225-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) to learn more.</span></span>
