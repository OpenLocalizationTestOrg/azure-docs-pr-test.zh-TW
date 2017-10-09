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
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="09812-103">Azure Service Fabric 中的 DNS 服務</span><span class="sxs-lookup"><span data-stu-id="09812-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="09812-104">hello DNS 服務是選用的系統服務，您可以在叢集 toodiscover 啟動其他服務使用 hello DNS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="09812-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="09812-105">許多服務，特別是容器化服務，可以有現有的 URL 名稱，而且可以 tooresolve 它們使用 hello 標準 DNS 通訊協定 （而非 hello 命名服務通訊協定） 是恰當的特別是在 「 提起和 shift 」 案例。</span><span class="sxs-lookup"><span data-stu-id="09812-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="09812-106">hello DNS 服務可讓您 toomap DNS 名稱 tooa 服務名稱，並因此解決端點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09812-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="09812-107">hello DNS 服務對應 DNS 名稱 tooservice 名稱，接著解析 hello 命名服務 tooreturn hello 服務端點。</span><span class="sxs-lookup"><span data-stu-id="09812-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="09812-108">hello hello 服務的 DNS 名稱是在建立 hello 時提供。</span><span class="sxs-lookup"><span data-stu-id="09812-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![服務端點][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="09812-110">啟用 hello DNS 服務</span><span class="sxs-lookup"><span data-stu-id="09812-110">Enabling hello DNS service</span></span>
<span data-ttu-id="09812-111">首先您必須在叢集中 tooenable hello DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="09812-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="09812-112">您想 toodeploy hello 叢集取得 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="09812-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="09812-113">可以是使用 hello[範例範本](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)或建立資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="09812-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="09812-114">您可以啟用 hello DNS 服務以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="09812-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="09812-115">請檢查該 hello`apiversion`設定得`2017-07-01-preview`hello`Microsoft.ServiceFabric/clusters`資源，並且如果沒有，請在 hello 下列程式碼片段所示更新它：</span><span class="sxs-lookup"><span data-stu-id="09812-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="09812-116">現在加入 hello 下列啟用 hello DNS 服務`addonFeatures`後面 hello 區段`fabricSettings`區段 hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="09812-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="09812-117">一旦您已更新您的叢集範本以 hello 上述變更，套用它們，並讓 hello 升級已完成。</span><span class="sxs-lookup"><span data-stu-id="09812-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="09812-118">Hello DNS 系統服務完成之後，開始執行在叢集中稱為`fabric:/System/DnsService`hello Service Fabric 總管 中的系統服務區段底下。</span><span class="sxs-lookup"><span data-stu-id="09812-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="09812-119">或者，您可以在叢集建立 hello 時間啟用 hello 透過 hello 入口網站的 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="09812-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="09812-120">您可以啟用 hello DNS 服務檢查 hello 方塊`Include DNS service`hello 中`Cluster configuration`功能表 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="09812-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![啟用透過 hello 入口網站的 DNS 服務][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="09812-122">設定您的服務的 hello DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="09812-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="09812-123">一旦 hello DNS 服務，正在您的叢集，您可以設定您的服務的 DNS 名稱以宣告方式的預設服務在 hello`ApplicationManifest.xml`或透過 Powershell 命令。</span><span class="sxs-lookup"><span data-stu-id="09812-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="09812-124">在 hello ApplicationManifest.xml 中設定的預設服務的 hello DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="09812-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="09812-125">開啟您的專案，在 Visual Studio 中或您偏好的編輯器，並開啟 hello`ApplicationManifest.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="09812-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="09812-126">移 toohello 預設服務 > 一節，以及每個服務加入 hello`ServiceDnsName`屬性。</span><span class="sxs-lookup"><span data-stu-id="09812-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="09812-127">hello 下列範例顯示如何 tooset hello hello 服務 DNS 名稱太`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="09812-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="09812-128">Hello 應用程式部署之後，hello Service Fabric 總管 中的 hello 服務執行個體就會顯示 hello DNS 名稱，這個執行個體，hello 遵循圖所示：</span><span class="sxs-lookup"><span data-stu-id="09812-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![服務端點][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="09812-130">設定服務，使用 Powershell 的 hello DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="09812-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="09812-131">您可以設定 hello 服務的 DNS 名稱，是在建立使用 hello `New-ServiceFabricService` Powershell。</span><span class="sxs-lookup"><span data-stu-id="09812-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="09812-132">hello 下列範例會建立新的無狀態服務 hello DNS 名稱`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="09812-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="09812-133">在您的服務中使用 DNS</span><span class="sxs-lookup"><span data-stu-id="09812-133">Using DNS in your services</span></span>
<span data-ttu-id="09812-134">如果您部署多個服務，您可以找到與其他服務 toocommunicate hello 端點使用的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="09812-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="09812-135">hello DNS 服務才適用 toostateless 服務，因為 hello DNS 通訊協定無法與可設定狀態的服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="09812-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="09812-136">可設定狀態服務，您可以使用 hello 內建的反向 proxy 的 http 呼叫 toocall 特定服務磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="09812-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="09812-137">hello 下列程式碼會示範如何 toocall 另一個服務，也就是只在一般的 http 呼叫其中 hello URL 的一部分提供 hello 連接埠以及任何選擇性路徑。</span><span class="sxs-lookup"><span data-stu-id="09812-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="09812-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09812-138">Next steps</span></span>
<span data-ttu-id="09812-139">深入了解與 hello 叢集內的服務通訊[連接，並與服務通訊](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="09812-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
