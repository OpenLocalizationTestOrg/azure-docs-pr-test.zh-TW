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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="1a99b-103">協助保護 Azure Service Fabric 中服務的通訊安全</span><span class="sxs-lookup"><span data-stu-id="1a99b-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a99b-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="1a99b-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="1a99b-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="1a99b-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="1a99b-106">安全性是 hello 通訊的最重要的層面的其中一個。</span><span class="sxs-lookup"><span data-stu-id="1a99b-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="1a99b-107">hello 可靠的服務應用程式架構會提供數的預先建立的通訊堆疊，您可以使用 tooimprove 安全性工具。</span><span class="sxs-lookup"><span data-stu-id="1a99b-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="1a99b-108">本文示範如何 tooimprove 時您所使用的安全性服務遠端處理和 hello Windows Communication Foundation (WCF) 通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="1a99b-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="1a99b-109">協助保護使用服務遠端處理時的服務安全</span><span class="sxs-lookup"><span data-stu-id="1a99b-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="1a99b-110">我們將使用的現有[範例](service-fabric-reliable-services-communication-remoting.md)，說明如何 tooset 向上可靠的服務的遠端處理功能。</span><span class="sxs-lookup"><span data-stu-id="1a99b-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="1a99b-111">toohelp 保護服務，而您使用服務遠端處理時，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1a99b-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="1a99b-112">建立介面， `IHelloWorldStateful`，定義可供您服務上的遠端程序呼叫的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="1a99b-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="1a99b-113">您的服務會使用`FabricTransportServiceRemotingListener`，宣告於 hello`Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime`命名空間。</span><span class="sxs-lookup"><span data-stu-id="1a99b-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="1a99b-114">這是提供遠端功能的 `ICommunicationListener` 實作。</span><span class="sxs-lookup"><span data-stu-id="1a99b-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="1a99b-115">新增接聽程式設定和安全性認證。</span><span class="sxs-lookup"><span data-stu-id="1a99b-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="1a99b-116">請確定您想要 toouse toohelp 安全 hello 叢集中的所有 hello 節點已安裝的服務通訊的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="1a99b-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="1a99b-117">有兩種方式可提供接聽程式設定和安全性認證：</span><span class="sxs-lookup"><span data-stu-id="1a99b-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="1a99b-118">直接在 hello 服務程式碼中提供：</span><span class="sxs-lookup"><span data-stu-id="1a99b-118">Provide them directly in hello service code:</span></span>

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
   2. <span data-ttu-id="1a99b-119">使用 [組態封裝](service-fabric-application-model.md)提供它們：</span><span class="sxs-lookup"><span data-stu-id="1a99b-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="1a99b-120">新增`TransportSettings`hello settings.xml 檔案中的區段。</span><span class="sxs-lookup"><span data-stu-id="1a99b-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="1a99b-121">在此情況下，hello`CreateServiceReplicaListeners`方法看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1a99b-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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

        <span data-ttu-id="1a99b-122">如果您將加入`TransportSettings`在 hello settings.xml 檔案中，區段`FabricTransportRemotingListenerSettings `會從本節載入所有 hello 設定預設。</span><span class="sxs-lookup"><span data-stu-id="1a99b-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="1a99b-123">在此情況下，hello`CreateServiceReplicaListeners`方法看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1a99b-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="1a99b-124">當您呼叫方法的安全服務上使用 hello 遠端處理堆疊，而不是使用 hello`Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy`類別 toocreate 服務 proxy，使用`Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`。</span><span class="sxs-lookup"><span data-stu-id="1a99b-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="1a99b-125">傳入包含 `SecurityCredentials` 的 `FabricTransportRemotingSettings`。</span><span class="sxs-lookup"><span data-stu-id="1a99b-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

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

    <span data-ttu-id="1a99b-126">如果 hello 用戶端程式碼做為服務一部分執行，您可以載入`FabricTransportRemotingSettings`hello settings.xml 檔案中。</span><span class="sxs-lookup"><span data-stu-id="1a99b-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="1a99b-127">建立 HelloWorldClientTransportSettings 區段是類似的 toohello 服務程式碼，如先前所示。</span><span class="sxs-lookup"><span data-stu-id="1a99b-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="1a99b-128">進行下列變更 toohello 用戶端程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="1a99b-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="1a99b-129">如果 hello 用戶端不以服務的一部分執行，您可以建立 client_name.settings.xml 檔案 hello hello client_name.exe 所在的相同位置。</span><span class="sxs-lookup"><span data-stu-id="1a99b-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="1a99b-130">然後在該檔案中建立 TransportSettings 區段。</span><span class="sxs-lookup"><span data-stu-id="1a99b-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="1a99b-131">類似 toohello 服務，如果您將加入`TransportSettings`> 一節中用戶端 settings.xml/client_name.settings.xml`FabricTransportRemotingSettings`預設載入本節中的 hello 的所有設定。</span><span class="sxs-lookup"><span data-stu-id="1a99b-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="1a99b-132">在此情況下，hello 先前的程式碼會更進一步簡化：</span><span class="sxs-lookup"><span data-stu-id="1a99b-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="1a99b-133">協助保護使用 WCF 通訊堆疊時的服務安全</span><span class="sxs-lookup"><span data-stu-id="1a99b-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="1a99b-134">我們將使用的現有[範例](service-fabric-reliable-services-communication-wcf.md)，說明如何 tooset WCF 為基礎的通訊堆疊，讓您可靠的服務。</span><span class="sxs-lookup"><span data-stu-id="1a99b-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="1a99b-135">toohelp 保護服務，而當您使用 WCF 為基礎的通訊堆疊，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1a99b-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="1a99b-136">Hello 服務，您需要 toohelp 安全 hello WCF 通訊接聽程式 (`WcfCommunicationListener`) 所建立。</span><span class="sxs-lookup"><span data-stu-id="1a99b-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="1a99b-137">toodo，修改 hello`CreateServiceReplicaListeners`方法。</span><span class="sxs-lookup"><span data-stu-id="1a99b-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

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
2. <span data-ttu-id="1a99b-138">在 hello client hello`WcfCommunicationClient`類別中所建立 hello 先前[範例](service-fabric-reliable-services-communication-wcf.md)維持不變。</span><span class="sxs-lookup"><span data-stu-id="1a99b-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="1a99b-139">但您需要 toooverride hello`CreateClientAsync`方法`WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="1a99b-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

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

    <span data-ttu-id="1a99b-140">使用`SecureWcfCommunicationClientFactory`toocreate WCF 通訊的用戶端 (`WcfCommunicationClient`)。</span><span class="sxs-lookup"><span data-stu-id="1a99b-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="1a99b-141">使用 hello 用戶端 tooinvoke 服務方法。</span><span class="sxs-lookup"><span data-stu-id="1a99b-141">Use hello client tooinvoke service methods.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1a99b-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a99b-142">Next steps</span></span>
* [<span data-ttu-id="1a99b-143">在 Reliable Services 中搭配 OWIN 使用 Web API</span><span class="sxs-lookup"><span data-stu-id="1a99b-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
