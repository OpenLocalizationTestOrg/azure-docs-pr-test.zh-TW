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
# <a name="enable-communication-for-role-instances-in-azure"></a>啟用 Azure 中角色執行個體的通訊
雲端服務角色透過內部和外部連線通訊。 外部連接稱為**輸入端點**，而內部連接稱為**內部端點**。 本主題描述如何 toomodify hello[服務定義](cloud-services-model-and-package.md#csdef)toocreate 端點。

## <a name="input-endpoint"></a>輸入端點
當您想 tooexpose 外部連接埠 toohello 時，會使用 hello 輸入的端點。 您指定 hello 通訊協定類型和 hello hello 端點便會套用兩個 hello 外部和內部連接埠 hello 端點連接埠。 如果您想，您可以指定 hello 端點不同的內部連接埠以 hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint)屬性。

hello 輸入的端點可以使用下列通訊協定的 hello: **http、 https、 tcp、 udp**。

toocreate 輸入端點，新增 hello **InputEndpoint**子元素 toohello**端點**web 或背景工作角色的項目。

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>執行個體輸入端點
執行個體輸入的端點類似 tooinput 端點，但可讓您將每個個別的角色執行個體的特定公開連接埠對應 hello 負載平衡器上使用連接埠轉送。 您可以指定單一公眾連接埠，或某個範圍內的連接埠。

只能使用 hello 執行個體輸入的端點**tcp**或**udp**做為 hello 通訊協定。

toocreate 執行個體輸入端點，新增 hello **InstanceInputEndpoint**子元素 toohello**端點**web 或背景工作角色的項目。

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>內部端點
內部端點可供執行個體對執行個體通訊時使用。 hello 連接埠為選擇性，而且 toohello 端點時，如果省略，要指派的動態通訊埠。 可以使用連接埠範圍。 每個角色的限制為五個內部端點。

hello 內部端點可以使用下列通訊協定的 hello: **http、 tcp、 udp、 任何**。

toocreate 內部輸入端點，新增 hello **InternalEndpoint**子元素 toohello**端點**web 或背景工作角色的項目。

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

您也可以使用連接埠範圍。

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>背景工作角色與Web 角色
使用背景工作角色和 Web 角色二者時端點會有一個很小的差異。 hello web 角色必須至少使用 hello 的單一輸入的端點**HTTP**通訊協定。

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>使用 hello.NET SDK tooaccess 端點
hello Azure Managed 程式庫提供在執行階段的角色執行個體 toocommunicate 方法。 從角色執行個體中執行的程式碼，您可以擷取 hello 存在其他角色執行個體以及其端點，以及 hello 目前角色執行個體的相關資訊。

> [!NOTE]
> 您只能抓取在您的雲端服務中執行，且至少定義一個內部端點之角色執行個體的相關資訊。 您無法取得在其他服務中執行之角色執行個體的相關資料。
> 
> 

您可以使用 hello[執行個體](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx)屬性 tooretrieve 角色執行個體。 第一次使用 hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn 參考 toohello 目前角色執行個體，然後再使用 hello[角色](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx)屬性 tooreturn 參考 toohello 角色本身。

當您以程式設計方式透過 hello.NET SDK 連線 tooa 角色執行個體時，是相當容易 tooaccess hello 端點資訊。 比方說，您已經連接 tooa 特定角色環境之後，您可以取得具有此程式碼的特定端點的 hello 連接埠：

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

hello**執行個體**屬性傳回的集合**RoleInstance**物件。 這個集合一定包含 hello 目前執行個體。 如果 hello 角色沒有定義內部端點，hello 集合會包含 hello 目前執行個體，但其他執行個體。 hello hello 集合中的角色執行個體數目一律為 hello 角色沒有任何內部端點定義所在的 hello 案例中為 1。 如果 hello 角色定義內部端點，其執行個體是在執行階段，可探索和 hello hello 集合中的執行個體數目將會對應 toohello hello 角色 hello 服務組態檔中指定的執行個體的數目。

> [!NOTE]
> hello Azure Managed 程式庫不提供方法來決定 hello 健全狀況的其他角色執行個體，但您可以實作這類的健康情況評估自行如果您的服務需要這項功能。 您可以使用[Azure 診斷](cloud-services-dotnet-diagnostics.md)tooobtain 資訊執行角色執行個體。
> 
> 

toodetermine hello 的角色執行個體上的內部端點的通訊埠編號，您可以使用 hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx)屬性 tooreturn 字典物件，其中包含端點名稱和它們對應的 IP 位址和連接埠。 hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx)屬性會傳回 hello IP 位址和連接埠指定的端點。 hello **PublicIPEndpoint**屬性會傳回負載平衡端點的 hello 連接埠。 hello hello IP 位址部分**PublicIPEndpoint**屬性不使用。

以下是逐一查看角色執行個體的範例。

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

以下是取得 hello 服務定義會公開 hello 端點並開始接聽連接的背景工作角色的範例。

> [!WARNING]
> 這個程式碼只適用於已部署的服務。 當在 hello Azure 計算模擬器中執行，服務會建立直接連接埠端點的組態項目 (**InstanceInputEndpoint**項目) 會被忽略。
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a>網路流量規則 toocontrol 角色通訊
定義內部端點之後，您可以新增網路流量的規則 （根據您所建立的 hello 端點） toocontrol 角色執行個體可以如何與彼此通訊。 hello 下圖顯示控制角色通訊的一些常見案例：

![網路流量規則案例](./media/cloud-services-enable-communication-role-instances/scenarios.png "網路流量規則案例")

hello 下列程式碼範例顯示 hello 如上圖所示的 hello 角色的角色定義。 每個角色定義都包含至少一個內部端點定義：

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
> 固定和自動指派之連接埠二者的內部端點都可能會在角色之間產生通訊限制。
> 
> 

根據預設，定義內部端點之後，通訊可以資料流程從任何角色 toohello 內部端點的角色沒有任何限制。 您必須新增 toorestrict 通訊**NetworkTrafficRules**元素 toohello **ServiceDefinition** hello 服務定義檔中的項目。

### <a name="scenario-1"></a>案例 1
只允許從網路流量**WebRole1**太**WorkerRole1**。

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

### <a name="scenario-2"></a>案例 2
只允許從網路流量**WebRole1**太**WorkerRole1**和**WorkerRole2**。

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

### <a name="scenario-3"></a>案例 3
只允許從網路流量**WebRole1**太**WorkerRole1**，和**WorkerRole1**太**WorkerRole2**。

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

### <a name="scenario-4"></a>案例 4
只允許從網路流量**WebRole1**太**WorkerRole1**， **WebRole1**太**WorkerRole2**，和**WorkerRole1**太**WorkerRole2**。

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

可以找到 hello 上面使用的項目 XML 結構描述參考[這裡](https://msdn.microsoft.com/library/azure/gg557551.aspx)。

## <a name="next-steps"></a>後續步驟
深入了解 hello 雲端服務[模型](cloud-services-model-and-package.md)。

