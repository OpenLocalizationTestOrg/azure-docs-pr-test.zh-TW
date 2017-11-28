---
title: "雲端服務中的角色 aaaCommunication |Microsoft 文件"
description: "雲端服務中的角色執行個體可以有端點 （http、 https、 tcp、 udp） 為其定義與 hello 外部或其他角色執行個體之間進行通訊。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="92b57-103">啟用 Azure 中角色執行個體的通訊</span><span class="sxs-lookup"><span data-stu-id="92b57-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="92b57-104">雲端服務角色透過內部和外部連線通訊。</span><span class="sxs-lookup"><span data-stu-id="92b57-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="92b57-105">外部連接稱為**輸入端點**，而內部連接稱為**內部端點**。</span><span class="sxs-lookup"><span data-stu-id="92b57-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="92b57-106">本主題描述如何 toomodify hello[服務定義](cloud-services-model-and-package.md#csdef)toocreate 端點。</span><span class="sxs-lookup"><span data-stu-id="92b57-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="92b57-107">輸入端點</span><span class="sxs-lookup"><span data-stu-id="92b57-107">Input endpoint</span></span>
<span data-ttu-id="92b57-108">當您想 tooexpose 外部連接埠 toohello 時，會使用 hello 輸入的端點。</span><span class="sxs-lookup"><span data-stu-id="92b57-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="92b57-109">您指定 hello 通訊協定類型和 hello hello 端點便會套用兩個 hello 外部和內部連接埠 hello 端點連接埠。</span><span class="sxs-lookup"><span data-stu-id="92b57-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="92b57-110">如果您想，您可以指定 hello 端點不同的內部連接埠以 hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint)屬性。</span><span class="sxs-lookup"><span data-stu-id="92b57-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="92b57-111">hello 輸入的端點可以使用下列通訊協定的 hello: **http、 https、 tcp、 udp**。</span><span class="sxs-lookup"><span data-stu-id="92b57-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="92b57-112">toocreate 輸入端點，新增 hello **InputEndpoint**子元素 toohello**端點**web 或背景工作角色的項目。</span><span class="sxs-lookup"><span data-stu-id="92b57-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="92b57-113">執行個體輸入端點</span><span class="sxs-lookup"><span data-stu-id="92b57-113">Instance input endpoint</span></span>
<span data-ttu-id="92b57-114">執行個體輸入的端點類似 tooinput 端點，但可讓您將每個個別的角色執行個體的特定公開連接埠對應 hello 負載平衡器上使用連接埠轉送。</span><span class="sxs-lookup"><span data-stu-id="92b57-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="92b57-115">您可以指定單一公眾連接埠，或某個範圍內的連接埠。</span><span class="sxs-lookup"><span data-stu-id="92b57-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="92b57-116">只能使用 hello 執行個體輸入的端點**tcp**或**udp**做為 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="92b57-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="92b57-117">toocreate 執行個體輸入端點，新增 hello **InstanceInputEndpoint**子元素 toohello**端點**web 或背景工作角色的項目。</span><span class="sxs-lookup"><span data-stu-id="92b57-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="92b57-118">內部端點</span><span class="sxs-lookup"><span data-stu-id="92b57-118">Internal endpoint</span></span>
<span data-ttu-id="92b57-119">內部端點可供執行個體對執行個體通訊時使用。</span><span class="sxs-lookup"><span data-stu-id="92b57-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="92b57-120">hello 連接埠為選擇性，而且 toohello 端點時，如果省略，要指派的動態通訊埠。</span><span class="sxs-lookup"><span data-stu-id="92b57-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="92b57-121">可以使用連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="92b57-121">A port range can be used.</span></span> <span data-ttu-id="92b57-122">每個角色的限制為五個內部端點。</span><span class="sxs-lookup"><span data-stu-id="92b57-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="92b57-123">hello 內部端點可以使用下列通訊協定的 hello: **http、 tcp、 udp、 任何**。</span><span class="sxs-lookup"><span data-stu-id="92b57-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="92b57-124">toocreate 內部輸入端點，新增 hello **InternalEndpoint**子元素 toohello**端點**web 或背景工作角色的項目。</span><span class="sxs-lookup"><span data-stu-id="92b57-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="92b57-125">您也可以使用連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="92b57-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="92b57-126">背景工作角色與Web 角色</span><span class="sxs-lookup"><span data-stu-id="92b57-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="92b57-127">使用背景工作角色和 Web 角色二者時端點會有一個很小的差異。</span><span class="sxs-lookup"><span data-stu-id="92b57-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="92b57-128">hello web 角色必須至少使用 hello 的單一輸入的端點**HTTP**通訊協定。</span><span class="sxs-lookup"><span data-stu-id="92b57-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="92b57-129">使用 hello.NET SDK tooaccess 端點</span><span class="sxs-lookup"><span data-stu-id="92b57-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="92b57-130">hello Azure Managed 程式庫提供在執行階段的角色執行個體 toocommunicate 方法。</span><span class="sxs-lookup"><span data-stu-id="92b57-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="92b57-131">從角色執行個體中執行的程式碼，您可以擷取 hello 存在其他角色執行個體以及其端點，以及 hello 目前角色執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="92b57-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="92b57-132">您只能抓取在您的雲端服務中執行，且至少定義一個內部端點之角色執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="92b57-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="92b57-133">您無法取得在其他服務中執行之角色執行個體的相關資料。</span><span class="sxs-lookup"><span data-stu-id="92b57-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="92b57-134">您可以使用 hello[執行個體](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx)屬性 tooretrieve 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="92b57-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="92b57-135">第一次使用 hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn 參考 toohello 目前角色執行個體，然後再使用 hello[角色](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx)屬性 tooreturn 參考 toohello 角色本身。</span><span class="sxs-lookup"><span data-stu-id="92b57-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="92b57-136">當您以程式設計方式透過 hello.NET SDK 連線 tooa 角色執行個體時，是相當容易 tooaccess hello 端點資訊。</span><span class="sxs-lookup"><span data-stu-id="92b57-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="92b57-137">比方說，您已經連接 tooa 特定角色環境之後，您可以取得具有此程式碼的特定端點的 hello 連接埠：</span><span class="sxs-lookup"><span data-stu-id="92b57-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="92b57-138">hello**執行個體**屬性傳回的集合**RoleInstance**物件。</span><span class="sxs-lookup"><span data-stu-id="92b57-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="92b57-139">這個集合一定包含 hello 目前執行個體。</span><span class="sxs-lookup"><span data-stu-id="92b57-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="92b57-140">如果 hello 角色沒有定義內部端點，hello 集合會包含 hello 目前執行個體，但其他執行個體。</span><span class="sxs-lookup"><span data-stu-id="92b57-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="92b57-141">hello hello 集合中的角色執行個體數目一律為 hello 角色沒有任何內部端點定義所在的 hello 案例中為 1。</span><span class="sxs-lookup"><span data-stu-id="92b57-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="92b57-142">如果 hello 角色定義內部端點，其執行個體是在執行階段，可探索和 hello hello 集合中的執行個體數目將會對應 toohello hello 角色 hello 服務組態檔中指定的執行個體的數目。</span><span class="sxs-lookup"><span data-stu-id="92b57-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="92b57-143">hello Azure Managed 程式庫不提供方法來決定 hello 健全狀況的其他角色執行個體，但您可以實作這類的健康情況評估自行如果您的服務需要這項功能。</span><span class="sxs-lookup"><span data-stu-id="92b57-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="92b57-144">您可以使用[Azure 診斷](cloud-services-dotnet-diagnostics.md)tooobtain 資訊執行角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="92b57-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="92b57-145">toodetermine hello 的角色執行個體上的內部端點的通訊埠編號，您可以使用 hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx)屬性 tooreturn 字典物件，其中包含端點名稱和它們對應的 IP 位址和連接埠。</span><span class="sxs-lookup"><span data-stu-id="92b57-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="92b57-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx)屬性會傳回 hello IP 位址和連接埠指定的端點。</span><span class="sxs-lookup"><span data-stu-id="92b57-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="92b57-147">hello **PublicIPEndpoint**屬性會傳回負載平衡端點的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="92b57-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="92b57-148">hello hello IP 位址部分**PublicIPEndpoint**屬性不使用。</span><span class="sxs-lookup"><span data-stu-id="92b57-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="92b57-149">以下是逐一查看角色執行個體的範例。</span><span class="sxs-lookup"><span data-stu-id="92b57-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="92b57-150">以下是取得 hello 服務定義會公開 hello 端點並開始接聽連接的背景工作角色的範例。</span><span class="sxs-lookup"><span data-stu-id="92b57-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="92b57-151">這個程式碼只適用於已部署的服務。</span><span class="sxs-lookup"><span data-stu-id="92b57-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="92b57-152">當在 hello Azure 計算模擬器中執行，服務會建立直接連接埠端點的組態項目 (**InstanceInputEndpoint**項目) 會被忽略。</span><span class="sxs-lookup"><span data-stu-id="92b57-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="92b57-153">網路流量規則 toocontrol 角色通訊</span><span class="sxs-lookup"><span data-stu-id="92b57-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="92b57-154">定義內部端點之後，您可以新增網路流量的規則 （根據您所建立的 hello 端點） toocontrol 角色執行個體可以如何與彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="92b57-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="92b57-155">hello 下圖顯示控制角色通訊的一些常見案例：</span><span class="sxs-lookup"><span data-stu-id="92b57-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="92b57-156">![網路流量規則案例](./media/cloud-services-enable-communication-role-instances/scenarios.png "網路流量規則案例")</span><span class="sxs-lookup"><span data-stu-id="92b57-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="92b57-157">hello 下列程式碼範例顯示 hello 如上圖所示的 hello 角色的角色定義。</span><span class="sxs-lookup"><span data-stu-id="92b57-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="92b57-158">每個角色定義都包含至少一個內部端點定義：</span><span class="sxs-lookup"><span data-stu-id="92b57-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="92b57-159">固定和自動指派之連接埠二者的內部端點都可能會在角色之間產生通訊限制。</span><span class="sxs-lookup"><span data-stu-id="92b57-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="92b57-160">根據預設，定義內部端點之後，通訊可以資料流程從任何角色 toohello 內部端點的角色沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="92b57-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="92b57-161">您必須新增 toorestrict 通訊**NetworkTrafficRules**元素 toohello **ServiceDefinition** hello 服務定義檔中的項目。</span><span class="sxs-lookup"><span data-stu-id="92b57-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="92b57-162">案例 1</span><span class="sxs-lookup"><span data-stu-id="92b57-162">Scenario 1</span></span>
<span data-ttu-id="92b57-163">只允許從網路流量**WebRole1**太**WorkerRole1**。</span><span class="sxs-lookup"><span data-stu-id="92b57-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="92b57-164">案例 2</span><span class="sxs-lookup"><span data-stu-id="92b57-164">Scenario 2</span></span>
<span data-ttu-id="92b57-165">只允許從網路流量**WebRole1**太**WorkerRole1**和**WorkerRole2**。</span><span class="sxs-lookup"><span data-stu-id="92b57-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="92b57-166">案例 3</span><span class="sxs-lookup"><span data-stu-id="92b57-166">Scenario 3</span></span>
<span data-ttu-id="92b57-167">只允許從網路流量**WebRole1**太**WorkerRole1**，和**WorkerRole1**太**WorkerRole2**。</span><span class="sxs-lookup"><span data-stu-id="92b57-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="92b57-168">案例 4</span><span class="sxs-lookup"><span data-stu-id="92b57-168">Scenario 4</span></span>
<span data-ttu-id="92b57-169">只允許從網路流量**WebRole1**太**WorkerRole1**， **WebRole1**太**WorkerRole2**，和**WorkerRole1**太**WorkerRole2**。</span><span class="sxs-lookup"><span data-stu-id="92b57-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="92b57-170">可以找到 hello 上面使用的項目 XML 結構描述參考[這裡](https://msdn.microsoft.com/library/azure/gg557551.aspx)。</span><span class="sxs-lookup"><span data-stu-id="92b57-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="92b57-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92b57-171">Next steps</span></span>
<span data-ttu-id="92b57-172">深入了解 hello 雲端服務[模型](cloud-services-model-and-package.md)。</span><span class="sxs-lookup"><span data-stu-id="92b57-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

