---
title: "Azure Service Fabric DNS 服務 | Microsoft Docs"
description: "使用 Service Fabric 的 DNS 服務來從叢集內部探索微服務。"
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
ms.openlocfilehash: 9871bc5aa4e74ab0faef401d67c4e9558eb5e14b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="b6906-103">Azure Service Fabric 中的 DNS 服務</span><span class="sxs-lookup"><span data-stu-id="b6906-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="b6906-104">「DNS 服務」是一個選用的系統服務，您可以在叢集中啟用以使用 DNS 通訊協定來探索其他服務。</span><span class="sxs-lookup"><span data-stu-id="b6906-104">The DNS Service is an optional system service that you can enable in your cluster to discover other services using the DNS protocol.</span></span>

<span data-ttu-id="b6906-105">許多服務 (特別是容器化服務) 都可以有現有的 URL 名稱，因此能夠使用標準 DNS 通訊協定 (而不是「命名服務」通訊協定) 來解析這些名稱，特別是在「隨即轉移」案例中。</span><span class="sxs-lookup"><span data-stu-id="b6906-105">Many services, especially containerized services, can have an existing URL name, and being able to resolve them using the standard DNS protocol (rather than the Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="b6906-106">DNS 服務可讓您將 DNS 服務對應到某個服務名稱，再由此解析端點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b6906-106">The DNS service enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="b6906-107">DNS 服務會將 DNS 名稱對應到服務名稱，接著服務名稱會由命名服務解析並傳回服務端點。</span><span class="sxs-lookup"><span data-stu-id="b6906-107">The DNS service maps DNS names to service names, which in turn are resolved by the Naming Service to return the service endpoint.</span></span> <span data-ttu-id="b6906-108">服務的 DNS 名稱是在建立時提供的。</span><span class="sxs-lookup"><span data-stu-id="b6906-108">The DNS name for the service is provided at the time of creation.</span></span> 

![服務端點][0]

## <a name="enabling-the-dns-service"></a><span data-ttu-id="b6906-110">啟用 DNS 服務</span><span class="sxs-lookup"><span data-stu-id="b6906-110">Enabling the DNS service</span></span>
<span data-ttu-id="b6906-111">首先，您必須在叢集啟用 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="b6906-111">First you need to enable the DNS service in your cluster.</span></span> <span data-ttu-id="b6906-112">取得您想要部署之叢集的範本。</span><span class="sxs-lookup"><span data-stu-id="b6906-112">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="b6906-113">您可以使用[範例範本](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)或建立 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="b6906-113">You can either use the [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="b6906-114">您可以使用下列步驟來啟用 DNS 服務：</span><span class="sxs-lookup"><span data-stu-id="b6906-114">You can enable the DNS service with the following steps:</span></span>

1. <span data-ttu-id="b6906-115">檢查 `Microsoft.ServiceFabric/clusters` 資源的 `apiversion` 是否已設定為 `2017-07-01-preview`，如果不是，請加以更新，如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="b6906-115">Check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in the following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="b6906-116">現在，在 `fabricSettings` 區段之後新增下列 `addonFeatures` 區段以啟用 DNS 服務，如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="b6906-116">Now enable the DNS service by adding the following `addonFeatures` section after the `fabricSettings` section as shown in the following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="b6906-117">一旦您使用前面的變更將叢集範本進行更新之後，將它們加以套用，使升級完成。</span><span class="sxs-lookup"><span data-stu-id="b6906-117">Once you have updated your cluster template with the preceding changes, apply them and let the upgrade complete.</span></span> <span data-ttu-id="b6906-118">完成之後，在 Service Fabric Explorer 的系統服務區段下，就有名為 `fabric:/System/DnsService` 的 DNS 系統服務在叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="b6906-118">Once complete, the DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in the Service Fabric explorer.</span></span> 

<span data-ttu-id="b6906-119">或者，您可以在叢集建立時，透過入口網站啟用 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="b6906-119">Alternatively, you can enable the DNS service through the portal at the time of cluster creation.</span></span> <span data-ttu-id="b6906-120">核取 `Cluster configuration`功能表中的 `Include DNS service` 方塊可啟用 DNS 服務，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="b6906-120">The DNS service can be enabled by checking the box for `Include DNS service` in the `Cluster configuration` menu as shown in the following screenshot:</span></span>

![透過入口網站啟用 DNS 服務][2]


## <a name="setting-the-dns-name-for-your-service"></a><span data-ttu-id="b6906-122">為您的服務設定 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="b6906-122">Setting the DNS name for your service</span></span>
<span data-ttu-id="b6906-123">一旦 DNS 服務已在您的叢集中執行，您現在便可以在 `ApplicationManifest.xml` 中透過宣告為預設服務設定 DNS 名稱，或透過 Powershell 命令為服務設定 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="b6906-123">Once the DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in the `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-the-dns-name-for-a-default-service-in-the-applicationmanifestxml"></a><span data-ttu-id="b6906-124">在 ApplicationManifest.xml 中為預設服務設定 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="b6906-124">Setting the DNS name for a default service in the ApplicationManifest.xml</span></span>
<span data-ttu-id="b6906-125">在 Visual Studio 或慣用的編輯器中開啟您的專案，然後開啟 `ApplicationManifest.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="b6906-125">Open your project in Visual Studio, or your favorite editor, and open the `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="b6906-126">移至預設服務區段，然後為每個服務新增 `ServiceDnsName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="b6906-126">Go to the default services section, and for each service add the `ServiceDnsName` attribute.</span></span> <span data-ttu-id="b6906-127">下列範例示範如何將服務的 DNS 名稱設定為 `service1.application1`</span><span class="sxs-lookup"><span data-stu-id="b6906-127">The following example shows how to set the DNS name of the service to `service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="b6906-128">部署完應用程式之後，在 Service Fabric Explorer 中的服務執行個體會顯示此執行個體的 DNS 名稱，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="b6906-128">Once the application is deployed, the service instance in the Service Fabric explorer shows the DNS name for this instance, as shown in the following figure:</span></span> 

![服務端點][1]

### <a name="setting-the-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="b6906-130">使用 Powershell 為服務設定 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="b6906-130">Setting the DNS name for a service using Powershell</span></span>
<span data-ttu-id="b6906-131">您可以在建立服務時，使用 `New-ServiceFabricService` Powershell 為服務設定 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="b6906-131">You can set the DNS name for a service when creating it using the `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="b6906-132">下列範例會建立 DNS 名稱為 `service1.application1` 的新無狀態服務</span><span class="sxs-lookup"><span data-stu-id="b6906-132">The following example creates a new stateless service with the DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="b6906-133">在您的服務中使用 DNS</span><span class="sxs-lookup"><span data-stu-id="b6906-133">Using DNS in your services</span></span>
<span data-ttu-id="b6906-134">如果您部署多個服務，您便可以使用 DNS 名稱來尋找要通訊對象的其他服務端點。</span><span class="sxs-lookup"><span data-stu-id="b6906-134">If you deploy more than one service, you can find the endpoints of other services to communicate with  by using a DNS name.</span></span> <span data-ttu-id="b6906-135">DNS 服務僅適用於無狀態服務，因為 DNS 通訊協定無法與具狀態服務通訊。</span><span class="sxs-lookup"><span data-stu-id="b6906-135">The DNS service is only applicable to stateless services, since the DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="b6906-136">針對具狀態服務，您可以使用 HTTP 呼叫的內建反向 Proxy 來呼叫特定的服務分割區。</span><span class="sxs-lookup"><span data-stu-id="b6906-136">For stateful services, you can use the built-in reverse proxy for http calls to call a particular service partition.</span></span>

<span data-ttu-id="b6906-137">下列程式碼會示範如何呼叫另一個服務，這只是一般的 HTTP 呼叫，其中您會提供連接埠和任何選用路徑作為 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="b6906-137">The following code shows how to call another service, which is simply a regular http call where you provide the port and any optional path as part of the URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b6906-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6906-138">Next steps</span></span>
<span data-ttu-id="b6906-139">若要深入了解叢集內的服務通訊，請參閱[連接服務並與其進行通訊](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="b6906-139">Learn more about service communication within the cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
