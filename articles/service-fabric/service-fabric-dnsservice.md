---
title: "服務網狀架構 DNS 服務 aaaAzure |Microsoft 文件"
description: "使用 Service Fabric dns 服務探索從 microservices hello 叢集內。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a>Azure Service Fabric 中的 DNS 服務
hello DNS 服務是選用的系統服務，您可以在叢集 toodiscover 啟動其他服務使用 hello DNS 通訊協定。

許多服務，特別是容器化服務，可以有現有的 URL 名稱，而且可以 tooresolve 它們使用 hello 標準 DNS 通訊協定 （而非 hello 命名服務通訊協定） 是恰當的特別是在 「 提起和 shift 」 案例。 hello DNS 服務可讓您 toomap DNS 名稱 tooa 服務名稱，並因此解決端點 IP 位址。 

hello DNS 服務對應 DNS 名稱 tooservice 名稱，接著解析 hello 命名服務 tooreturn hello 服務端點。 hello hello 服務的 DNS 名稱是在建立 hello 時提供。 

![服務端點][0]

## <a name="enabling-hello-dns-service"></a>啟用 hello DNS 服務
首先您必須在叢集中 tooenable hello DNS 服務。 您想 toodeploy hello 叢集取得 hello 範本。 可以是使用 hello[範例範本](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)或建立資源管理員範本。 您可以啟用 hello DNS 服務以 hello 下列步驟：

1. 請檢查該 hello`apiversion`設定得`2017-07-01-preview`hello`Microsoft.ServiceFabric/clusters`資源，並且如果沒有，請在 hello 下列程式碼片段所示更新它：

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. 現在加入 hello 下列啟用 hello DNS 服務`addonFeatures`後面 hello 區段`fabricSettings`區段 hello 下列程式碼片段所示： 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. 一旦您已更新您的叢集範本以 hello 上述變更，套用它們，並讓 hello 升級已完成。 Hello DNS 系統服務完成之後，開始執行在叢集中稱為`fabric:/System/DnsService`hello Service Fabric 總管 中的系統服務區段底下。 

或者，您可以在叢集建立 hello 時間啟用 hello 透過 hello 入口網站的 DNS 服務。 您可以啟用 hello DNS 服務檢查 hello 方塊`Include DNS service`hello 中`Cluster configuration`功能表 hello 下列螢幕擷取畫面所示：

![啟用透過 hello 入口網站的 DNS 服務][2]


## <a name="setting-hello-dns-name-for-your-service"></a>設定您的服務的 hello DNS 名稱
一旦 hello DNS 服務，正在您的叢集，您可以設定您的服務的 DNS 名稱以宣告方式的預設服務在 hello`ApplicationManifest.xml`或透過 Powershell 命令。

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>在 hello ApplicationManifest.xml 中設定的預設服務的 hello DNS 名稱
開啟您的專案，在 Visual Studio 中或您偏好的編輯器，並開啟 hello`ApplicationManifest.xml`檔案。 移 toohello 預設服務 > 一節，以及每個服務加入 hello`ServiceDnsName`屬性。 hello 下列範例顯示如何 tooset hello hello 服務 DNS 名稱太`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Hello 應用程式部署之後，hello Service Fabric 總管 中的 hello 服務執行個體就會顯示 hello DNS 名稱，這個執行個體，hello 遵循圖所示： 

![服務端點][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>設定服務，使用 Powershell 的 hello DNS 名稱
您可以設定 hello 服務的 DNS 名稱，是在建立使用 hello `New-ServiceFabricService` Powershell。 hello 下列範例會建立新的無狀態服務 hello DNS 名稱`service1.application1`

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a>在您的服務中使用 DNS
如果您部署多個服務，您可以找到與其他服務 toocommunicate hello 端點使用的 DNS 名稱。 hello DNS 服務才適用 toostateless 服務，因為 hello DNS 通訊協定無法與可設定狀態的服務進行通訊。 可設定狀態服務，您可以使用 hello 內建的反向 proxy 的 http 呼叫 toocall 特定服務磁碟分割。

hello 下列程式碼會示範如何 toocall 另一個服務，也就是只在一般的 http 呼叫其中 hello URL 的一部分提供 hello 連接埠以及任何選擇性路徑。

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a>後續步驟
深入了解與 hello 叢集內的服務通訊[連接，並與服務通訊](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
