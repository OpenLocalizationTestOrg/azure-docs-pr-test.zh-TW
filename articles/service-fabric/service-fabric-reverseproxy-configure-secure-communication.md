---
title: "Azure Service Fabric 反向 Proxy 安全通訊 | Microsoft Docs"
description: "設定反向 Proxy，以確保安全的端對端通訊。"
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
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: 568f9638c59282bcd7d3fae058a1588a889c22dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a><span data-ttu-id="5ed8f-103">安全服務與反向 Proxy 的連線</span><span class="sxs-lookup"><span data-stu-id="5ed8f-103">Connect to a secure service with the reverse proxy</span></span>

<span data-ttu-id="5ed8f-104">本文說明如何建立反向 Proxy 和服務之間的安全連線，以確保端對端的安全通道。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-104">This article explains how to establish secure connection between the reverse proxy and services, thus enabling an end to end secure channel.</span></span>

<span data-ttu-id="5ed8f-105">僅有將反向 Proxy 設為接聽 HTTPS 時，才支援安全的服務連線。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-105">Connecting to secure services is supported only when reverse proxy is configured to listen on HTTPS.</span></span> <span data-ttu-id="5ed8f-106">本文件的其餘部分均假設上述情況成立。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-106">Rest of the document assumes this is the case.</span></span>
<span data-ttu-id="5ed8f-107">若要設定 Service Fabric 中的反向 Proxy，請參閱 [Azure Service Fabric 中的反向 Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-107">Refer to [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) to configure the reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a><span data-ttu-id="5ed8f-108">建立反向 Proxy 與服務之間的安全連線</span><span class="sxs-lookup"><span data-stu-id="5ed8f-108">Secure connection establishment between the reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-to-services"></a><span data-ttu-id="5ed8f-109">服務的反向 Proxy 驗證：</span><span class="sxs-lookup"><span data-stu-id="5ed8f-109">Reverse proxy authenticating to services:</span></span>
<span data-ttu-id="5ed8f-110">反向 Proxy 可藉由憑證讓服務對其進行識別，該憑證是使用[資源類型區段](../azure-resource-manager/resource-group-authoring-templates.md)中 [叢集] 的 ***reverseProxyCertificate*** 屬性來指定。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-110">The reverse proxy identifies itself to services using its certificate, specified with ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="5ed8f-111">服務可以實作邏輯來驗證反向 Proxy 出示的憑證。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-111">Services can implement the logic to verify the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="5ed8f-112">服務可以將接受的用戶端憑證詳細資料指定為設定套件中的組態設定。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-112">The services can specify the accepted client certificate details as configuration settings in the configuration package.</span></span> <span data-ttu-id="5ed8f-113">系統會在執行階段時加以讀取，並用來驗證反向 Proxy 出示的憑證。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-113">This can be read at runtime and used to validate the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="5ed8f-114">若要新增組態設定，請參閱[管理應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-114">Refer to [Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) to add the configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a><span data-ttu-id="5ed8f-115">反向 Proxy 可透過服務出示的憑證，來驗證服務的身分識別：</span><span class="sxs-lookup"><span data-stu-id="5ed8f-115">Reverse proxy verifying the service's identity via the certificate presented by the service:</span></span>
<span data-ttu-id="5ed8f-116">若要針對服務出示的憑證執行伺服器憑證驗證，反向 Proxy 需支援 None、ServiceCommonNameAndIssuer 和 ServiceCertificateThumbprints 其中一個選項。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-116">To perform server certificate validation of the certificates presented by the services, reverse proxy supports one of the following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="5ed8f-117">若要選擇上述三個選項之一，請在 [fabricSettings](service-fabric-cluster-fabric-settings.md) 下方 ApplicationGateway/Http 項目的參數區段中指定 **ApplicationCertificateValidationPolicy**。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-117">To select one of these three options, specify the **ApplicationCertificateValidationPolicy** in the parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="5ed8f-118">如需每個選項的其他設定詳細資訊，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-118">Refer to the next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="5ed8f-119">服務憑證驗證選項</span><span class="sxs-lookup"><span data-stu-id="5ed8f-119">Service certificate validation options</span></span> 

- <span data-ttu-id="5ed8f-120">**None**：反向 Proxy 會略過驗證透過 Proxy 的服務憑證，並建立安全連線。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-120">**None**: Reverse proxy skips verification of the proxied service certificate and establishes the secure connection.</span></span> <span data-ttu-id="5ed8f-121">此為預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-121">This is the default behavior.</span></span>
<span data-ttu-id="5ed8f-122">在 ApplicationGateway/Http 項目的參數區段中，為 **ApplicationCertificateValidationPolicy** 指定 **None** 值。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-122">Specify the **ApplicationCertificateValidationPolicy** with value **None** in the parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="5ed8f-123">**ServiceCommonNameAndIssuer**：反向 Proxy 會依據憑證的通用名稱和直接簽發者的指紋，來驗證服務出示的憑證：在 ApplicationGateway/Http 項目的參數區段中，為 **ApplicationCertificateValidationPolicy** 指定 **ServiceCommonNameAndIssuer** 值。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies the certificate presented by the service based on certificate's common name and immediate issuer's thumbprint: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in the parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="5ed8f-124">若要指定服務的通用名稱和簽發者指紋清單，請在 fabricSettings 下方新增 **ApplicationGateway/Http/ServiceCommonNameAndIssuer** 項目，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-124">To specify the list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="5ed8f-125">您可在參數陣列項目中新增多組憑證通用名稱和簽發者指紋。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-125">Multiple certificate common name and issuer thumbprint pairs can be added in the parameters array element.</span></span> 

<span data-ttu-id="5ed8f-126">當反向 Proxy 要連接某個端點時，若該端點出示的憑證通用名稱和簽發者指紋符合此處指定的任何值，即會建立 SSL 通道。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-126">If the endpoint reverse proxy is connecting to presents a certificate who's common name and  issuer thumbprint matches any of the values specified here, SSL channel is established.</span></span> <span data-ttu-id="5ed8f-127">如果憑證詳細資料比對發生錯誤，反向 Proxy 就無法完成用戶端的要求，並會顯示狀態碼 502 (閘道錯誤)。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-127">Upon failure to match the certificate details, reverse proxy fails the client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="5ed8f-128">HTTP 狀態行也會出現「SSL 憑證無效」的句子。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-128">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span> 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- <span data-ttu-id="5ed8f-129">**ServiceCertificateThumbprints**：反向 Proxy 會依據透過 Proxy 之服務的指紋來驗證其憑證。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-129">**ServiceCertificateThumbprints**: Reverse proxy will verify the proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="5ed8f-130">當服務設為使用自我簽署憑證時，您可以選擇採用此路由：在 ApplicationGateway/Http 項目的參數區段中，為 **ApplicationCertificateValidationPolicy** 指定 **ServiceCertificateThumbprints** 值。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-130">You can choose to go this route when the services are configured with self signed certificates: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in the parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="5ed8f-131">另外，請在 ApplicationGateway/Http 項目的參數區段下方，為指紋指定 **ServiceCertificateThumbprints** 項目。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-131">Also specify the thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="5ed8f-132">您可以在值欄位中，以逗號分隔的清單來指定多個指紋，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5ed8f-132">Multiple thumbprints can be specified as a comma-separated list in the value field, as shown below:</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="5ed8f-133">如果這個設定項目中有列入伺服器憑證的指紋，反向 Proxy 的 SSL 連線即可成功。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-133">If the thumbprint of the server certificate is listed in this config entry, reverse proxy succeeds the SSL connection.</span></span> <span data-ttu-id="5ed8f-134">否則，它會終止連線而無法完成用戶端的要求，並顯示 502 (閘道錯誤)。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-134">Otherwise, it terminates the connection and fails the client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="5ed8f-135">HTTP 狀態行也會出現「SSL 憑證無效」的句子。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-135">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="5ed8f-136">當服務公開安全與不安全端點時的端點選取邏輯</span><span class="sxs-lookup"><span data-stu-id="5ed8f-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="5ed8f-137">Service Fabric 支援設定多個服務端點。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="5ed8f-138">請參閱[在服務資訊清單中指定資源](service-fabric-service-manifest-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="5ed8f-139">反向 Proxy 會依據 **ListenerName** 查詢參數，來選取其中一個用來轉送要求的端點。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-139">Reverse proxy selects one of the endpoints to forward the request based on the  **ListenerName** query parameter.</span></span> <span data-ttu-id="5ed8f-140">如果未指定該參數，它就會從端點清單中挑選任一端點。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-140">If this is not specified, it can pick any endpoint from the endpoints list.</span></span> <span data-ttu-id="5ed8f-141">現在，這可能是 HTTP 或 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="5ed8f-142">有時候，您可能希望/需要反向 Proxy 在「僅限安全模式」中運作，好比說，</span><span class="sxs-lookup"><span data-stu-id="5ed8f-142">There might be scenarios/requirements where you want the reverse proxy to operate in a "secure only mode", i.e</span></span> <span data-ttu-id="5ed8f-143">您不希望安全的反向 Proxy 將要求轉送到不安全的端點。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-143">you don't want the secure reverse proxy to forward requests to unsecured endpoints.</span></span> <span data-ttu-id="5ed8f-144">若要達成上述目標，您可在 ApplicationGateway/Http 項目的參數區段中，為 **SecureOnlyMode** 設定項目指定 **true** 值。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-144">This can be achieved by specifying the **SecureOnlyMode** configuration entry with value **true** in the parameters section of ApplicationGateway/Http element.</span></span>   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> <span data-ttu-id="5ed8f-145">在 **SecureOnlyMode** 中運作時，如果用戶端指定的 **ListenerName** 是對應至 HTTP (不安全) 端點，則反向 Proxy 無法完成要求，並會顯示 HTTP 狀態碼 404 (找不到)。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding to an HTTP(unsecured) endpoint, reverse proxy fails the request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a><span data-ttu-id="5ed8f-146">設定透過反向 Proxy 的用戶端憑證驗證</span><span class="sxs-lookup"><span data-stu-id="5ed8f-146">Setting up client certificate authentication through the reverse proxy</span></span>
<span data-ttu-id="5ed8f-147">當反向 Proxy 端發生 SSL 終止時，所有用戶端憑證資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-147">SSL termination happens at the reverse proxy and all the client certificate data is lost.</span></span> <span data-ttu-id="5ed8f-148">若要讓服務執行用戶端憑證驗證，請在 ApplicationGateway/Http 項目的參數區段中，進行 **ForwardClientCertificate** 設定。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-148">For the services to perform client certificate authentication, set the **ForwardClientCertificate** setting in the parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="5ed8f-149">如果 **ForwardClientCertificate** 設為 **false**，則在反向 Proxy 與用戶端的 SSL 交握期間，將不會要求用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-149">When **ForwardClientCertificate** is set to **false**, reverse proxy will not request for the client certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="5ed8f-150">此為預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-150">This is the default behavior.</span></span>

2. <span data-ttu-id="5ed8f-151">如果 **ForwardClientCertificate** 設為 **true**，則在反向 Proxy 與用戶端的 SSL 交握期間，會要求用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-151">When **ForwardClientCertificate** is set to **true**, reverse proxy requests for the client's certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="5ed8f-152">接著，它會使用名為 **X-Client-Certificate** 的自訂 HTTP 標頭來轉送用戶端憑證資料。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-152">It will then forward the client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="5ed8f-153">標頭值是用戶端憑證的 PEM 格式字串 (base64 編碼)。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-153">The header value is the base64 encoded PEM format string of the client's certificate.</span></span> <span data-ttu-id="5ed8f-154">檢查憑證資料之後，服務或許能成功完成要求，也可能無法完成要求，並顯示適當的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-154">The service can succeed/fail the request with appropriate status code after inspecting the certificate data.</span></span>
<span data-ttu-id="5ed8f-155">如果用戶端未出示憑證，反向 Proxy 會轉送空白標頭，以讓服務處理這種情況。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-155">If the client does not present a certificate, reverse proxy forwards an empty header and let the service handle the case.</span></span>

> <span data-ttu-id="5ed8f-156">反向 Proxy 只是個轉寄站。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="5ed8f-157">它不會執行任何用戶端憑證的驗證。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-157">It will not perform any validation of the client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ed8f-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ed8f-158">Next steps</span></span>
* <span data-ttu-id="5ed8f-159">如需 Azure Resource Manager 範本範例，以便使用不同的服務憑證驗證選項來設定安全反向 Proxy，請參閱[設定反向 Proxy 以連接安全的服務](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services)。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-159">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="5ed8f-160">請參閱 [GitHub 上的範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)中服務之間的 HTTP 通訊範例。</span><span class="sxs-lookup"><span data-stu-id="5ed8f-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="5ed8f-161">使用 Reliable Services 遠端服務進行遠端程序呼叫</span><span class="sxs-lookup"><span data-stu-id="5ed8f-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="5ed8f-162">在 Reliable Services 中使用 OWIN 的 Web API</span><span class="sxs-lookup"><span data-stu-id="5ed8f-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="5ed8f-163">管理叢集憑證</span><span class="sxs-lookup"><span data-stu-id="5ed8f-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
