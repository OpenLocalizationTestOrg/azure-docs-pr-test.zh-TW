---
title: "Service Fabric aaaAzure 反向 proxy 安全通訊 |Microsoft 文件"
description: "設定反向 proxy tooenable 的端對端通訊安全。"
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
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="ddd29-103">Tooa 安全服務連接與 hello 反向 proxy</span><span class="sxs-lookup"><span data-stu-id="ddd29-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="ddd29-104">本文說明如何 tooestablish 安全 hello 反向 proxy 與服務，因此能夠結束 tooend 安全通道之間的連線。</span><span class="sxs-lookup"><span data-stu-id="ddd29-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="ddd29-105">Toosecure 服務連線反向 proxy 是在 HTTPS 上的設定的 toolisten 時，才支援。</span><span class="sxs-lookup"><span data-stu-id="ddd29-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="ddd29-106">Hello 文件的其餘部分會假設為 hello 情況。</span><span class="sxs-lookup"><span data-stu-id="ddd29-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="ddd29-107">請參閱太[反向 proxy，在 Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello 反向 proxy 服務網狀架構中的。</span><span class="sxs-lookup"><span data-stu-id="ddd29-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="ddd29-108">Hello 反向 proxy 與服務之間建立安全的連線</span><span class="sxs-lookup"><span data-stu-id="ddd29-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="ddd29-109">反向 proxy 驗證 tooservices:</span><span class="sxs-lookup"><span data-stu-id="ddd29-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="ddd29-110">hello 反向 proxy 會將自己識別使用其憑證，以指定 tooservices ***reverseProxyCertificate***屬性在 hello**叢集**[資源類型] 區段](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ddd29-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="ddd29-111">服務可以實作 hello 邏輯 tooverify hello 憑證 hello 反向 proxy 來呈現。</span><span class="sxs-lookup"><span data-stu-id="ddd29-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="ddd29-112">hello 服務可以指定 hello 接受用戶端憑證的詳細資訊，為 hello 組態封裝中的組態設定。</span><span class="sxs-lookup"><span data-stu-id="ddd29-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="ddd29-113">這可以在執行階段讀取，而且用來顯示 hello 反向 proxy toovalidate hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="ddd29-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="ddd29-114">請參閱太[管理應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)tooadd hello 組態設定。</span><span class="sxs-lookup"><span data-stu-id="ddd29-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="ddd29-115">反向 proxy 驗證透過 hello 憑證由 hello 服務所提供的 hello 服務的身分識別：</span><span class="sxs-lookup"><span data-stu-id="ddd29-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="ddd29-116">tooperform 伺服器憑證驗證的 hello hello 服務所提供的憑證，反向 proxy 支援一個 hello 下列選項： None、 ServiceCommonNameAndIssuer 和 ServiceCertificateThumbprints。</span><span class="sxs-lookup"><span data-stu-id="ddd29-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="ddd29-117">tooselect 這三個選項，其中指定 hello **ApplicationCertificateValidationPolicy** ApplicationGateway/Http 項目底下的 hello 參數區段中[fabricSettings](service-fabric-cluster-fabric-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd29-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="ddd29-118">如需有關每個這些選項的其他組態的詳細資訊，請參閱 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="ddd29-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="ddd29-119">服務憑證驗證選項</span><span class="sxs-lookup"><span data-stu-id="ddd29-119">Service certificate validation options</span></span> 

- <span data-ttu-id="ddd29-120">**無**： 反向 proxy 略過驗證的 hello 代理服務憑證，以及建立 hello 安全連線。</span><span class="sxs-lookup"><span data-stu-id="ddd29-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="ddd29-121">這是 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="ddd29-121">This is hello default behavior.</span></span>
<span data-ttu-id="ddd29-122">指定 hello **ApplicationCertificateValidationPolicy**值**無**ApplicationGateway/Http 項目的 hello 參數區段中。</span><span class="sxs-lookup"><span data-stu-id="ddd29-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="ddd29-123">**ServiceCommonNameAndIssuer**: hello 憑證根據憑證的一般名稱] 和 [即時運算的簽發者指紋 hello 服務所提供的反向 proxy 驗證： 指定 hello **ApplicationCertificateValidationPolicy**值**ServiceCommonNameAndIssuer** ApplicationGateway/Http 項目的 hello 參數區段中。</span><span class="sxs-lookup"><span data-stu-id="ddd29-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="ddd29-124">服務的一般名稱和簽發者指紋 toospecify hello 清單新增**ApplicationGateway/Http/ServiceCommonNameAndIssuer**項目底下 fabricSettings，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ddd29-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="ddd29-125">Hello 參數陣列項目可以加入多個憑證一般名稱和簽發者指紋組。</span><span class="sxs-lookup"><span data-stu-id="ddd29-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="ddd29-126">如果 hello 端點反向 proxy 連接 toopresents 身為一般的憑證名稱和簽發者指紋符合任何 hello 此處指定的值，會建立 SSL 通道。</span><span class="sxs-lookup"><span data-stu-id="ddd29-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="ddd29-127">失敗 toomatch hello 憑證詳細資料，在反向 proxy 失敗 （不正確的閘道） 狀態碼 502 hello 用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="ddd29-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="ddd29-128">hello HTTP 狀態行也會包含 hello 片語 「 無效 SSL 憑證。 」</span><span class="sxs-lookup"><span data-stu-id="ddd29-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="ddd29-129">**ServiceCertificateThumbprints**： 反向 proxy 會驗證其指紋為依據的 hello 代理服務憑證。</span><span class="sxs-lookup"><span data-stu-id="ddd29-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="ddd29-130">您可以選擇 toogo 此路由 hello 服務設定為自我簽署憑證時： 指定 hello **ApplicationCertificateValidationPolicy**值**ServiceCertificateThumbprints**ApplicationGateway/Http 項目的 hello 參數區段中。</span><span class="sxs-lookup"><span data-stu-id="ddd29-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="ddd29-131">也會指定與 hello 指紋**ServiceCertificateThumbprints** ApplicationGateway/Http 項目的 [參數] 區段下的項目。</span><span class="sxs-lookup"><span data-stu-id="ddd29-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="ddd29-132">可以為在 hello 值欄位中，以逗號分隔清單指定多個指紋，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ddd29-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

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

<span data-ttu-id="ddd29-133">如果 hello hello 伺服器憑證指紋列為這個組態項目中，反向 proxy 成功 hello SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="ddd29-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="ddd29-134">否則，它所終止 hello 連線和失敗 hello 與 502 （不正確的閘道） 的用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="ddd29-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="ddd29-135">hello HTTP 狀態行也會包含 hello 片語 「 無效 SSL 憑證。 」</span><span class="sxs-lookup"><span data-stu-id="ddd29-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="ddd29-136">當服務公開安全與不安全端點時的端點選取邏輯</span><span class="sxs-lookup"><span data-stu-id="ddd29-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="ddd29-137">Service Fabric 支援設定多個服務端點。</span><span class="sxs-lookup"><span data-stu-id="ddd29-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="ddd29-138">請參閱[在服務資訊清單中指定資源](service-fabric-service-manifest-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd29-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="ddd29-139">反向 proxy 會選取其中一個 hello 端點 tooforward hello 要求根據 hello **ListenerName**查詢參數。</span><span class="sxs-lookup"><span data-stu-id="ddd29-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="ddd29-140">如果未指定此參數，它可以挑選任何端點從 hello 端點清單。</span><span class="sxs-lookup"><span data-stu-id="ddd29-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="ddd29-141">現在，這可能是 HTTP 或 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="ddd29-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="ddd29-142">可能有案例/需求想 hello 反向 proxy toooperate 中 「 安全模式 」，也就是</span><span class="sxs-lookup"><span data-stu-id="ddd29-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="ddd29-143">您不想 hello 安全的反向 proxy tooforward 要求 toounsecured 端點。</span><span class="sxs-lookup"><span data-stu-id="ddd29-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="ddd29-144">這可藉由指定 hello **SecureOnlyMode**值的組態項目**true** ApplicationGateway/Http 項目的 hello 參數區段中。</span><span class="sxs-lookup"><span data-stu-id="ddd29-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="ddd29-145">在操作時**SecureOnlyMode**，如果已指定用戶端**ListenerName**對應 tooan HTTP(unsecured) 端點的反向 proxy 失敗 hello 要求以 404 （找不到） 的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="ddd29-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="ddd29-146">設定用戶端憑證驗證，透過 hello 反向 proxy</span><span class="sxs-lookup"><span data-stu-id="ddd29-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="ddd29-147">SSL 終止會發生在 hello 反向 proxy，而且所有 hello 用戶端憑證資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="ddd29-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="ddd29-148">Hello 服務 tooperform 用戶端憑證驗證，設定 hello **ForwardClientCertificate** ApplicationGateway/Http 項目的 hello 參數區段中設定。</span><span class="sxs-lookup"><span data-stu-id="ddd29-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="ddd29-149">當**ForwardClientCertificate**設定得**false**、 反向 proxy 將不會要求 hello 用戶端憑證的 SSL 交握期間與 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ddd29-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="ddd29-150">這是 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="ddd29-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="ddd29-151">當**ForwardClientCertificate**設定得**true**，hello 用戶端使用其 SSL 交握期間反向 proxy 要求 hello 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ddd29-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="ddd29-152">它會再轉送 hello 用戶端憑證資料中名為自訂 HTTP 標頭**X 用戶端憑證**。</span><span class="sxs-lookup"><span data-stu-id="ddd29-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="ddd29-153">hello 標頭值為 hello hello 用戶端憑證的 base64 編碼 PEM 格式字串。</span><span class="sxs-lookup"><span data-stu-id="ddd29-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="ddd29-154">hello 服務可以成功/失敗 hello 要求，適當的狀態碼之後檢查 hello 憑證資料。</span><span class="sxs-lookup"><span data-stu-id="ddd29-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="ddd29-155">Hello 用戶端不會顯示憑證，如果反向 proxy 是空的標頭，並且讓 hello 服務控制代碼 hello 的情況。</span><span class="sxs-lookup"><span data-stu-id="ddd29-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="ddd29-156">反向 Proxy 只是個轉寄站。</span><span class="sxs-lookup"><span data-stu-id="ddd29-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="ddd29-157">它不會執行任何驗證的 hello 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ddd29-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ddd29-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddd29-158">Next steps</span></span>
* <span data-ttu-id="ddd29-159">請參閱太[設定反向 proxy tooconnect toosecure 服務](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services)Azure 資源管理員的範本範例 tooconfigure 安全反向 proxy hello 不同的服務憑證驗證選項。</span><span class="sxs-lookup"><span data-stu-id="ddd29-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="ddd29-160">請參閱 [GitHub 上的範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)中服務之間的 HTTP 通訊範例。</span><span class="sxs-lookup"><span data-stu-id="ddd29-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="ddd29-161">使用 Reliable Services 遠端服務進行遠端程序呼叫</span><span class="sxs-lookup"><span data-stu-id="ddd29-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="ddd29-162">在 Reliable Services 中使用 OWIN 的 Web API</span><span class="sxs-lookup"><span data-stu-id="ddd29-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="ddd29-163">管理叢集憑證</span><span class="sxs-lookup"><span data-stu-id="ddd29-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
