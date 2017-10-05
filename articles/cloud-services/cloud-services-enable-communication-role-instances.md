---
title: "雲端服務中角色的通訊 | Microsoft Docs"
description: "您可以為雲端服務中的角色執行個體定義端點 (http、https、tcp、udp)，以便與外部或在其他角色執行個體之間通訊。"
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
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="778c4-103">啟用 Azure 中角色執行個體的通訊</span><span class="sxs-lookup"><span data-stu-id="778c4-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="778c4-104">雲端服務角色透過內部和外部連線通訊。</span><span class="sxs-lookup"><span data-stu-id="778c4-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="778c4-105">外部連接稱為**輸入端點**，而內部連接稱為**內部端點**。</span><span class="sxs-lookup"><span data-stu-id="778c4-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="778c4-106">本主題描述如何修改 [服務定義](cloud-services-model-and-package.md#csdef) 以建立端點。</span><span class="sxs-lookup"><span data-stu-id="778c4-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="778c4-107">輸入端點</span><span class="sxs-lookup"><span data-stu-id="778c4-107">Input endpoint</span></span>
<span data-ttu-id="778c4-108">輸入端點是在您要對外公開連接埠時使用。</span><span class="sxs-lookup"><span data-stu-id="778c4-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="778c4-109">您可以指定通訊協定類型端點連接埠，稍後這些連接埠將套用至端點的外部和內部連接埠。</span><span class="sxs-lookup"><span data-stu-id="778c4-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="778c4-110">您也可以使用 [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) 屬性為端點指定不同的內部連接埠。</span><span class="sxs-lookup"><span data-stu-id="778c4-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="778c4-111">輸入端點可以使用下列通訊協定： **http、https、tcp、udp**。</span><span class="sxs-lookup"><span data-stu-id="778c4-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="778c4-112">若要建立輸入端點，請將 **InputEndpoint** 子元素新增至 Web 或背景工作角色的 **Endpoints** 元素。</span><span class="sxs-lookup"><span data-stu-id="778c4-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="778c4-113">執行個體輸入端點</span><span class="sxs-lookup"><span data-stu-id="778c4-113">Instance input endpoint</span></span>
<span data-ttu-id="778c4-114">執行個體輸入端點與輸入端點類似，但可讓您使用負載平衡器上的連接埠轉送，來針對各角色執行個體對應特定的公眾連接埠。</span><span class="sxs-lookup"><span data-stu-id="778c4-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="778c4-115">您可以指定單一公眾連接埠，或某個範圍內的連接埠。</span><span class="sxs-lookup"><span data-stu-id="778c4-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="778c4-116">執行個體輸入端點只能使用 **tcp** 或 **udp** 作為通訊協定。</span><span class="sxs-lookup"><span data-stu-id="778c4-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="778c4-117">若要建立執行個體輸入端點，請將 **InstanceInputEndpoint** 子元素新增至 Web 或背景工作角色的 **Endpoints** 元素。</span><span class="sxs-lookup"><span data-stu-id="778c4-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="778c4-118">內部端點</span><span class="sxs-lookup"><span data-stu-id="778c4-118">Internal endpoint</span></span>
<span data-ttu-id="778c4-119">內部端點可供執行個體對執行個體通訊時使用。</span><span class="sxs-lookup"><span data-stu-id="778c4-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="778c4-120">該連接埠是選擇性的，如果省略，將指派動態連接埠至端點。</span><span class="sxs-lookup"><span data-stu-id="778c4-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="778c4-121">可以使用連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="778c4-121">A port range can be used.</span></span> <span data-ttu-id="778c4-122">每個角色的限制為五個內部端點。</span><span class="sxs-lookup"><span data-stu-id="778c4-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="778c4-123">內部端點可以使用下列通訊協定： **http、tcp、udp、any**。</span><span class="sxs-lookup"><span data-stu-id="778c4-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="778c4-124">若要建立內部輸入端點，請將 **InternalEndpoint** 子元素新增至 Web 或背景工作角色的 **Endpoints** 元素。</span><span class="sxs-lookup"><span data-stu-id="778c4-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="778c4-125">您也可以使用連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="778c4-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="778c4-126">背景工作角色與Web 角色</span><span class="sxs-lookup"><span data-stu-id="778c4-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="778c4-127">使用背景工作角色和 Web 角色二者時端點會有一個很小的差異。</span><span class="sxs-lookup"><span data-stu-id="778c4-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="778c4-128">Web 角色必須至少要有一個輸入端點使用 **HTTP** 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="778c4-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="778c4-129">使用 .NET SDK 存取端點</span><span class="sxs-lookup"><span data-stu-id="778c4-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="778c4-130">Azure 受管理程式庫提供讓角色執行個體在執行階段通訊的方法。</span><span class="sxs-lookup"><span data-stu-id="778c4-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="778c4-131">藉由在角色執行個體內執行的程式碼，您可以抓取角色執行個體及其端點之存在的相關資訊，以及目前角色執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="778c4-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="778c4-132">您只能抓取在您的雲端服務中執行，且至少定義一個內部端點之角色執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="778c4-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="778c4-133">您無法取得在其他服務中執行之角色執行個體的相關資料。</span><span class="sxs-lookup"><span data-stu-id="778c4-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="778c4-134">您可以使用 [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) 屬性抓取角色的執行個體。</span><span class="sxs-lookup"><span data-stu-id="778c4-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="778c4-135">先使用 [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) 以傳回對目前角色執行個體的參考，然後使用 [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) 屬性來傳回對角色本身的參考。</span><span class="sxs-lookup"><span data-stu-id="778c4-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="778c4-136">當您以程式設計方式透過 .NET SDK 連接到角色執行個體時，存取端點資訊就相對較簡單。</span><span class="sxs-lookup"><span data-stu-id="778c4-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="778c4-137">例如，當您連接到特定的角色環境後，即可使用此程式碼取得特定端點的連接埠：</span><span class="sxs-lookup"><span data-stu-id="778c4-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="778c4-138">**Instances** 屬性會傳回 **RoleInstance** 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="778c4-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="778c4-139">這個集合一律會包含目前的執行個體。</span><span class="sxs-lookup"><span data-stu-id="778c4-139">This collection always contains the current instance.</span></span> <span data-ttu-id="778c4-140">如果該角色沒有定義內部端點，則該集合只包含目前的執行個體，沒有其他執行個體。</span><span class="sxs-lookup"><span data-stu-id="778c4-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="778c4-141">在沒有為角色定義內部端點的情況下，集合中的角色執行個體數量一律為 1。</span><span class="sxs-lookup"><span data-stu-id="778c4-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="778c4-142">如果該角色定義了一個內部端點，就可以在執行階段中探索其執行個體，而且集合中執行個體的數量將與服務組態檔中為該角色指定的執行個體數量相對應。</span><span class="sxs-lookup"><span data-stu-id="778c4-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="778c4-143">Azure 設管理程式庫沒有提供判斷其他角色執行個體健康狀態的方法，但是如果您的服務需要這類功能，您可以自行實作此健康狀態評估。</span><span class="sxs-lookup"><span data-stu-id="778c4-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="778c4-144">您可以使用 [Azure 診斷](cloud-services-dotnet-diagnostics.md) 來取得執行中角色執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="778c4-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="778c4-145">若要判斷角色執行個體上內部端點的連接埠號碼，您可以使用 [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) 屬性，以傳回包含端點名稱及其對應 IP 位址與連接埠的 Dictionary 物件。</span><span class="sxs-lookup"><span data-stu-id="778c4-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="778c4-146">[IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) 屬性會傳回指定端點的 IP 位址和連接埠。</span><span class="sxs-lookup"><span data-stu-id="778c4-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="778c4-147">**PublicIPEndpoint** 屬性會傳回負載平衡端點的連接埠。</span><span class="sxs-lookup"><span data-stu-id="778c4-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="778c4-148">未使用 **PublicIPEndpoint** 屬性的 IP 位址部分。</span><span class="sxs-lookup"><span data-stu-id="778c4-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="778c4-149">以下是逐一查看角色執行個體的範例。</span><span class="sxs-lookup"><span data-stu-id="778c4-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="778c4-150">以下是可取得透過服務定義所公開的端點並開始接聽連線之背景工作角色的範例。</span><span class="sxs-lookup"><span data-stu-id="778c4-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="778c4-151">這個程式碼只適用於已部署的服務。</span><span class="sxs-lookup"><span data-stu-id="778c4-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="778c4-152">在 Azure 計算模擬器中執行時，會忽略建立直接連接埠 (**InstanceInputEndpoint** 元素) 的服務組態元素。</span><span class="sxs-lookup"><span data-stu-id="778c4-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
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
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="778c4-153">用網路流量規則控制角色通訊</span><span class="sxs-lookup"><span data-stu-id="778c4-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="778c4-154">定義內部端點之後，您可以新增網路流量規則 (根據建立的端點) 來控制角色之間通訊的方式。</span><span class="sxs-lookup"><span data-stu-id="778c4-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="778c4-155">下圖顯示一些控制角色通訊的常見案例：</span><span class="sxs-lookup"><span data-stu-id="778c4-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="778c4-156">![網路流量規則案例](./media/cloud-services-enable-communication-role-instances/scenarios.png "網路流量規則案例")</span><span class="sxs-lookup"><span data-stu-id="778c4-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="778c4-157">以下程式碼範例顯示上圖中角色的角色定義。</span><span class="sxs-lookup"><span data-stu-id="778c4-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="778c4-158">每個角色定義都包含至少一個內部端點定義：</span><span class="sxs-lookup"><span data-stu-id="778c4-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="778c4-159">固定和自動指派之連接埠二者的內部端點都可能會在角色之間產生通訊限制。</span><span class="sxs-lookup"><span data-stu-id="778c4-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="778c4-160">根據預設，定義內部端點之後，來自任何角色的通訊都可以在沒有任何限制的情況下流向角色的內部端點。</span><span class="sxs-lookup"><span data-stu-id="778c4-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="778c4-161">若要限制通訊，您必須在服務定義檔中將 **NetworkTrafficRules** 元素新增至 **ServiceDefinition** 元素。</span><span class="sxs-lookup"><span data-stu-id="778c4-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="778c4-162">案例 1</span><span class="sxs-lookup"><span data-stu-id="778c4-162">Scenario 1</span></span>
<span data-ttu-id="778c4-163">只允許從 **WebRole1** 至 **WorkerRole1** 的網路流量。</span><span class="sxs-lookup"><span data-stu-id="778c4-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="778c4-164">案例 2</span><span class="sxs-lookup"><span data-stu-id="778c4-164">Scenario 2</span></span>
<span data-ttu-id="778c4-165">只允許從 **WebRole1** 至 **WorkerRole1** 和 **WorkerRole2** 的網路流量。</span><span class="sxs-lookup"><span data-stu-id="778c4-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="778c4-166">案例 3</span><span class="sxs-lookup"><span data-stu-id="778c4-166">Scenario 3</span></span>
<span data-ttu-id="778c4-167">只允許從 **WebRole1** 至 **WorkerRole1**，以及從 **WorkerRole1** 至 **WorkerRole2** 的網路流量。</span><span class="sxs-lookup"><span data-stu-id="778c4-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="778c4-168">案例 4</span><span class="sxs-lookup"><span data-stu-id="778c4-168">Scenario 4</span></span>
<span data-ttu-id="778c4-169">只允許從 **WebRole1** 至 **WorkerRole1**、從 **WebRole1** 至 **WorkerRole2**，以及從 **WorkerRole1** 至 **WorkerRole2** 的網路流量。</span><span class="sxs-lookup"><span data-stu-id="778c4-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

<span data-ttu-id="778c4-170">[這裡](https://msdn.microsoft.com/library/azure/gg557551.aspx)有上數範例中使用之元素的 XML 結構描述參考。</span><span class="sxs-lookup"><span data-stu-id="778c4-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="778c4-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="778c4-171">Next steps</span></span>
<span data-ttu-id="778c4-172">深入了解雲端服務 [模型](cloud-services-model-and-package.md)。</span><span class="sxs-lookup"><span data-stu-id="778c4-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

