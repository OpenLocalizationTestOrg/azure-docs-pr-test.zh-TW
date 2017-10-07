---
title: "aaaHelp 中 Azure Service Fabric 服務的安全通訊 |Microsoft 文件"
description: "Azure Service Fabric 叢集中執行的方式 toohelp 安全可靠的服務通訊的概觀。"
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>協助保護 Azure Service Fabric 中服務的通訊安全
> [!div class="op_single_selector"]
> * [Windows 上的 C# ](service-fabric-reliable-services-secure-communication.md)
> * [在 Linux 上使用 Java](service-fabric-reliable-services-secure-communication-java.md)
>
>

安全性是 hello 通訊的最重要的層面的其中一個。 hello 可靠的服務應用程式架構會提供數的預先建立的通訊堆疊，您可以使用 tooimprove 安全性工具。 本文示範如何 tooimprove 時您所使用的安全性服務遠端處理和 hello Windows Communication Foundation (WCF) 通訊堆疊。

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>協助保護使用服務遠端處理時的服務安全
我們將使用的現有[範例](service-fabric-reliable-services-communication-remoting.md)，說明如何 tooset 向上可靠的服務的遠端處理功能。 toohelp 保護服務，而您使用服務遠端處理時，請遵循下列步驟：

1. 建立介面， `IHelloWorldStateful`，定義可供您服務上的遠端程序呼叫的 hello 方法。 您的服務會使用`FabricTransportServiceRemotingListener`，宣告於 hello`Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime`命名空間。 這是提供遠端功能的 `ICommunicationListener` 實作。

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. 新增接聽程式設定和安全性認證。

    請確定您想要 toouse toohelp 安全 hello 叢集中的所有 hello 節點已安裝的服務通訊的 hello 憑證。 有兩種方式可提供接聽程式設定和安全性認證：

   1. 直接在 hello 服務程式碼中提供：

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. 使用 [組態封裝](service-fabric-application-model.md)提供它們：

       新增`TransportSettings`hello settings.xml 檔案中的區段。

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       在此情況下，hello`CreateServiceReplicaListeners`方法看起來像這樣：

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        如果您將加入`TransportSettings`在 hello settings.xml 檔案中，區段`FabricTransportRemotingListenerSettings `會從本節載入所有 hello 設定預設。

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        在此情況下，hello`CreateServiceReplicaListeners`方法看起來像這樣：

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. 當您呼叫方法的安全服務上使用 hello 遠端處理堆疊，而不是使用 hello`Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy`類別 toocreate 服務 proxy，使用`Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`。 傳入包含 `SecurityCredentials` 的 `FabricTransportRemotingSettings`。

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    如果 hello 用戶端程式碼做為服務一部分執行，您可以載入`FabricTransportRemotingSettings`hello settings.xml 檔案中。 建立 HelloWorldClientTransportSettings 區段是類似的 toohello 服務程式碼，如先前所示。 進行下列變更 toohello 用戶端程式碼的 hello:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    如果 hello 用戶端不以服務的一部分執行，您可以建立 client_name.settings.xml 檔案 hello hello client_name.exe 所在的相同位置。 然後在該檔案中建立 TransportSettings 區段。

    類似 toohello 服務，如果您將加入`TransportSettings`> 一節中用戶端 settings.xml/client_name.settings.xml`FabricTransportRemotingSettings`預設載入本節中的 hello 的所有設定。

    在此情況下，hello 先前的程式碼會更進一步簡化：  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>協助保護使用 WCF 通訊堆疊時的服務安全
我們將使用的現有[範例](service-fabric-reliable-services-communication-wcf.md)，說明如何 tooset WCF 為基礎的通訊堆疊，讓您可靠的服務。 toohelp 保護服務，而當您使用 WCF 為基礎的通訊堆疊，請遵循下列步驟：

1. Hello 服務，您需要 toohelp 安全 hello WCF 通訊接聽程式 (`WcfCommunicationListener`) 所建立。 toodo，修改 hello`CreateServiceReplicaListeners`方法。

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in hello ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. 在 hello client hello`WcfCommunicationClient`類別中所建立 hello 先前[範例](service-fabric-reliable-services-communication-wcf.md)維持不變。 但您需要 toooverride hello`CreateClientAsync`方法`WcfCommunicationClientFactory`:

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    使用`SecureWcfCommunicationClientFactory`toocreate WCF 通訊的用戶端 (`WcfCommunicationClient`)。 使用 hello 用戶端 tooinvoke 服務方法。

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a>後續步驟
* [在 Reliable Services 中搭配 OWIN 使用 Web API](service-fabric-reliable-services-communication-webapi.md)
