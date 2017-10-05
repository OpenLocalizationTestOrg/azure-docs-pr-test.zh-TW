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
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a>安全服務與反向 Proxy 的連線

本文說明如何建立反向 Proxy 和服務之間的安全連線，以確保端對端的安全通道。

僅有將反向 Proxy 設為接聽 HTTPS 時，才支援安全的服務連線。 本文件的其餘部分均假設上述情況成立。
若要設定 Service Fabric 中的反向 Proxy，請參閱 [Azure Service Fabric 中的反向 Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)。

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a>建立反向 Proxy 與服務之間的安全連線 

### <a name="reverse-proxy-authenticating-to-services"></a>服務的反向 Proxy 驗證：
反向 Proxy 可藉由憑證讓服務對其進行識別，該憑證是使用[資源類型區段](../azure-resource-manager/resource-group-authoring-templates.md)中 [叢集] 的 ***reverseProxyCertificate*** 屬性來指定。 服務可以實作邏輯來驗證反向 Proxy 出示的憑證。 服務可以將接受的用戶端憑證詳細資料指定為設定套件中的組態設定。 系統會在執行階段時加以讀取，並用來驗證反向 Proxy 出示的憑證。 若要新增組態設定，請參閱[管理應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)。 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a>反向 Proxy 可透過服務出示的憑證，來驗證服務的身分識別：
若要針對服務出示的憑證執行伺服器憑證驗證，反向 Proxy 需支援 None、ServiceCommonNameAndIssuer 和 ServiceCertificateThumbprints 其中一個選項。
若要選擇上述三個選項之一，請在 [fabricSettings](service-fabric-cluster-fabric-settings.md) 下方 ApplicationGateway/Http 項目的參數區段中指定 **ApplicationCertificateValidationPolicy**。

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

如需每個選項的其他設定詳細資訊，請參閱下一節。

### <a name="service-certificate-validation-options"></a>服務憑證驗證選項 

- **None**：反向 Proxy 會略過驗證透過 Proxy 的服務憑證，並建立安全連線。 此為預設行為。
在 ApplicationGateway/Http 項目的參數區段中，為 **ApplicationCertificateValidationPolicy** 指定 **None** 值。

- **ServiceCommonNameAndIssuer**：反向 Proxy 會依據憑證的通用名稱和直接簽發者的指紋，來驗證服務出示的憑證：在 ApplicationGateway/Http 項目的參數區段中，為 **ApplicationCertificateValidationPolicy** 指定 **ServiceCommonNameAndIssuer** 值。

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

若要指定服務的通用名稱和簽發者指紋清單，請在 fabricSettings 下方新增 **ApplicationGateway/Http/ServiceCommonNameAndIssuer** 項目，如下所示。 您可在參數陣列項目中新增多組憑證通用名稱和簽發者指紋。 

當反向 Proxy 要連接某個端點時，若該端點出示的憑證通用名稱和簽發者指紋符合此處指定的任何值，即會建立 SSL 通道。 如果憑證詳細資料比對發生錯誤，反向 Proxy 就無法完成用戶端的要求，並會顯示狀態碼 502 (閘道錯誤)。 HTTP 狀態行也會出現「SSL 憑證無效」的句子。 

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


- **ServiceCertificateThumbprints**：反向 Proxy 會依據透過 Proxy 之服務的指紋來驗證其憑證。 當服務設為使用自我簽署憑證時，您可以選擇採用此路由：在 ApplicationGateway/Http 項目的參數區段中，為 **ApplicationCertificateValidationPolicy** 指定 **ServiceCertificateThumbprints** 值。

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

另外，請在 ApplicationGateway/Http 項目的參數區段下方，為指紋指定 **ServiceCertificateThumbprints** 項目。 您可以在值欄位中，以逗號分隔的清單來指定多個指紋，如下所示：

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

如果這個設定項目中有列入伺服器憑證的指紋，反向 Proxy 的 SSL 連線即可成功。 否則，它會終止連線而無法完成用戶端的要求，並顯示 502 (閘道錯誤)。 HTTP 狀態行也會出現「SSL 憑證無效」的句子。

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>當服務公開安全與不安全端點時的端點選取邏輯
Service Fabric 支援設定多個服務端點。 請參閱[在服務資訊清單中指定資源](service-fabric-service-manifest-resources.md)。

反向 Proxy 會依據 **ListenerName** 查詢參數，來選取其中一個用來轉送要求的端點。 如果未指定該參數，它就會從端點清單中挑選任一端點。 現在，這可能是 HTTP 或 HTTPS 端點。 有時候，您可能希望/需要反向 Proxy 在「僅限安全模式」中運作，好比說， 您不希望安全的反向 Proxy 將要求轉送到不安全的端點。 若要達成上述目標，您可在 ApplicationGateway/Http 項目的參數區段中，為 **SecureOnlyMode** 設定項目指定 **true** 值。   

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
> 在 **SecureOnlyMode** 中運作時，如果用戶端指定的 **ListenerName** 是對應至 HTTP (不安全) 端點，則反向 Proxy 無法完成要求，並會顯示 HTTP 狀態碼 404 (找不到)。

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a>設定透過反向 Proxy 的用戶端憑證驗證
當反向 Proxy 端發生 SSL 終止時，所有用戶端憑證資料都會遺失。 若要讓服務執行用戶端憑證驗證，請在 ApplicationGateway/Http 項目的參數區段中，進行 **ForwardClientCertificate** 設定。

1. 如果 **ForwardClientCertificate** 設為 **false**，則在反向 Proxy 與用戶端的 SSL 交握期間，將不會要求用戶端憑證。
此為預設行為。

2. 如果 **ForwardClientCertificate** 設為 **true**，則在反向 Proxy 與用戶端的 SSL 交握期間，會要求用戶端憑證。
接著，它會使用名為 **X-Client-Certificate** 的自訂 HTTP 標頭來轉送用戶端憑證資料。 標頭值是用戶端憑證的 PEM 格式字串 (base64 編碼)。 檢查憑證資料之後，服務或許能成功完成要求，也可能無法完成要求，並顯示適當的狀態碼。
如果用戶端未出示憑證，反向 Proxy 會轉送空白標頭，以讓服務處理這種情況。

> 反向 Proxy 只是個轉寄站。 它不會執行任何用戶端憑證的驗證。


## <a name="next-steps"></a>後續步驟
* 如需 Azure Resource Manager 範本範例，以便使用不同的服務憑證驗證選項來設定安全反向 Proxy，請參閱[設定反向 Proxy 以連接安全的服務](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services)。
* 請參閱 [GitHub 上的範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)中服務之間的 HTTP 通訊範例。
* [使用 Reliable Services 遠端服務進行遠端程序呼叫](service-fabric-reliable-services-communication-remoting.md)
* [在 Reliable Services 中使用 OWIN 的 Web API](service-fabric-reliable-services-communication-webapi.md)
* [管理叢集憑證](service-fabric-cluster-security-update-certs-azure.md)
