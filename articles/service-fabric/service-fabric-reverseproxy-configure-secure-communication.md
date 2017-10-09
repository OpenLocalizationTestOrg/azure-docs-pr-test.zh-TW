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
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Tooa 安全服務連接與 hello 反向 proxy

本文說明如何 tooestablish 安全 hello 反向 proxy 與服務，因此能夠結束 tooend 安全通道之間的連線。

Toosecure 服務連線反向 proxy 是在 HTTPS 上的設定的 toolisten 時，才支援。 Hello 文件的其餘部分會假設為 hello 情況。
請參閱太[反向 proxy，在 Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello 反向 proxy 服務網狀架構中的。

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Hello 反向 proxy 與服務之間建立安全的連線 

### <a name="reverse-proxy-authenticating-tooservices"></a>反向 proxy 驗證 tooservices:
hello 反向 proxy 會將自己識別使用其憑證，以指定 tooservices ***reverseProxyCertificate***屬性在 hello**叢集**[資源類型] 區段](../azure-resource-manager/resource-group-authoring-templates.md). 服務可以實作 hello 邏輯 tooverify hello 憑證 hello 反向 proxy 來呈現。 hello 服務可以指定 hello 接受用戶端憑證的詳細資訊，為 hello 組態封裝中的組態設定。 這可以在執行階段讀取，而且用來顯示 hello 反向 proxy toovalidate hello 憑證。 請參閱太[管理應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)tooadd hello 組態設定。 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>反向 proxy 驗證透過 hello 憑證由 hello 服務所提供的 hello 服務的身分識別：
tooperform 伺服器憑證驗證的 hello hello 服務所提供的憑證，反向 proxy 支援一個 hello 下列選項： None、 ServiceCommonNameAndIssuer 和 ServiceCertificateThumbprints。
tooselect 這三個選項，其中指定 hello **ApplicationCertificateValidationPolicy** ApplicationGateway/Http 項目底下的 hello 參數區段中[fabricSettings](service-fabric-cluster-fabric-settings.md)。

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

如需有關每個這些選項的其他組態的詳細資訊，請參閱 toohello 下一節。

### <a name="service-certificate-validation-options"></a>服務憑證驗證選項 

- **無**： 反向 proxy 略過驗證的 hello 代理服務憑證，以及建立 hello 安全連線。 這是 hello 預設行為。
指定 hello **ApplicationCertificateValidationPolicy**值**無**ApplicationGateway/Http 項目的 hello 參數區段中。

- **ServiceCommonNameAndIssuer**: hello 憑證根據憑證的一般名稱] 和 [即時運算的簽發者指紋 hello 服務所提供的反向 proxy 驗證： 指定 hello **ApplicationCertificateValidationPolicy**值**ServiceCommonNameAndIssuer** ApplicationGateway/Http 項目的 hello 參數區段中。

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

服務的一般名稱和簽發者指紋 toospecify hello 清單新增**ApplicationGateway/Http/ServiceCommonNameAndIssuer**項目底下 fabricSettings，如下所示。 Hello 參數陣列項目可以加入多個憑證一般名稱和簽發者指紋組。 

如果 hello 端點反向 proxy 連接 toopresents 身為一般的憑證名稱和簽發者指紋符合任何 hello 此處指定的值，會建立 SSL 通道。 失敗 toomatch hello 憑證詳細資料，在反向 proxy 失敗 （不正確的閘道） 狀態碼 502 hello 用戶端的要求。 hello HTTP 狀態行也會包含 hello 片語 「 無效 SSL 憑證。 」 

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


- **ServiceCertificateThumbprints**： 反向 proxy 會驗證其指紋為依據的 hello 代理服務憑證。 您可以選擇 toogo 此路由 hello 服務設定為自我簽署憑證時： 指定 hello **ApplicationCertificateValidationPolicy**值**ServiceCertificateThumbprints**ApplicationGateway/Http 項目的 hello 參數區段中。

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

也會指定與 hello 指紋**ServiceCertificateThumbprints** ApplicationGateway/Http 項目的 [參數] 區段下的項目。 可以為在 hello 值欄位中，以逗號分隔清單指定多個指紋，如下所示：

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

如果 hello hello 伺服器憑證指紋列為這個組態項目中，反向 proxy 成功 hello SSL 連線。 否則，它所終止 hello 連線和失敗 hello 與 502 （不正確的閘道） 的用戶端的要求。 hello HTTP 狀態行也會包含 hello 片語 「 無效 SSL 憑證。 」

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>當服務公開安全與不安全端點時的端點選取邏輯
Service Fabric 支援設定多個服務端點。 請參閱[在服務資訊清單中指定資源](service-fabric-service-manifest-resources.md)。

反向 proxy 會選取其中一個 hello 端點 tooforward hello 要求根據 hello **ListenerName**查詢參數。 如果未指定此參數，它可以挑選任何端點從 hello 端點清單。 現在，這可能是 HTTP 或 HTTPS 端點。 可能有案例/需求想 hello 反向 proxy toooperate 中 「 安全模式 」，也就是 您不想 hello 安全的反向 proxy tooforward 要求 toounsecured 端點。 這可藉由指定 hello **SecureOnlyMode**值的組態項目**true** ApplicationGateway/Http 項目的 hello 參數區段中。   

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
> 在操作時**SecureOnlyMode**，如果已指定用戶端**ListenerName**對應 tooan HTTP(unsecured) 端點的反向 proxy 失敗 hello 要求以 404 （找不到） 的 HTTP 狀態碼。

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>設定用戶端憑證驗證，透過 hello 反向 proxy
SSL 終止會發生在 hello 反向 proxy，而且所有 hello 用戶端憑證資料都會遺失。 Hello 服務 tooperform 用戶端憑證驗證，設定 hello **ForwardClientCertificate** ApplicationGateway/Http 項目的 hello 參數區段中設定。

1. 當**ForwardClientCertificate**設定得**false**、 反向 proxy 將不會要求 hello 用戶端憑證的 SSL 交握期間與 hello 用戶端。
這是 hello 預設行為。

2. 當**ForwardClientCertificate**設定得**true**，hello 用戶端使用其 SSL 交握期間反向 proxy 要求 hello 用戶端憑證。
它會再轉送 hello 用戶端憑證資料中名為自訂 HTTP 標頭**X 用戶端憑證**。 hello 標頭值為 hello hello 用戶端憑證的 base64 編碼 PEM 格式字串。 hello 服務可以成功/失敗 hello 要求，適當的狀態碼之後檢查 hello 憑證資料。
Hello 用戶端不會顯示憑證，如果反向 proxy 是空的標頭，並且讓 hello 服務控制代碼 hello 的情況。

> 反向 Proxy 只是個轉寄站。 它不會執行任何驗證的 hello 用戶端憑證。


## <a name="next-steps"></a>後續步驟
* 請參閱太[設定反向 proxy tooconnect toosecure 服務](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services)Azure 資源管理員的範本範例 tooconfigure 安全反向 proxy hello 不同的服務憑證驗證選項。
* 請參閱 [GitHub 上的範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)中服務之間的 HTTP 通訊範例。
* [使用 Reliable Services 遠端服務進行遠端程序呼叫](service-fabric-reliable-services-communication-remoting.md)
* [在 Reliable Services 中使用 OWIN 的 Web API](service-fabric-reliable-services-communication-webapi.md)
* [管理叢集憑證](service-fabric-cluster-security-update-certs-azure.md)
