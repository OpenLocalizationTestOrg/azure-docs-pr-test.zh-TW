---
title: "aaaHelp 中 Azure Service Fabric 服務的安全通訊 |Microsoft 文件"
description: "Azure Service Fabric 叢集中執行的方式 toohelp 安全可靠的服務通訊的概觀。"
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="f80fd-103">協助保護 Azure Service Fabric 中服務的通訊安全</span><span class="sxs-lookup"><span data-stu-id="f80fd-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f80fd-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="f80fd-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="f80fd-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="f80fd-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="f80fd-106">協助保護使用服務遠端處理時的服務安全</span><span class="sxs-lookup"><span data-stu-id="f80fd-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="f80fd-107">我們將使用的現有[範例](service-fabric-reliable-services-communication-remoting-java.md)，說明如何 tooset 向上可靠的服務的遠端處理功能。</span><span class="sxs-lookup"><span data-stu-id="f80fd-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="f80fd-108">toohelp 保護服務，而您使用服務遠端處理時，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f80fd-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="f80fd-109">建立介面， `HelloWorldStateless`，定義可供您服務上的遠端程序呼叫的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="f80fd-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="f80fd-110">您的服務會使用`FabricTransportServiceRemotingListener`，宣告於 hello`microsoft.serviceFabric.services.remoting.fabricTransport.runtime`封裝。</span><span class="sxs-lookup"><span data-stu-id="f80fd-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="f80fd-111">這是提供遠端功能的 `CommunicationListener` 實作。</span><span class="sxs-lookup"><span data-stu-id="f80fd-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="f80fd-112">新增接聽程式設定和安全性認證。</span><span class="sxs-lookup"><span data-stu-id="f80fd-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="f80fd-113">請確定您想要 toouse toohelp 安全 hello 叢集中的所有 hello 節點已安裝的服務通訊的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="f80fd-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="f80fd-114">有兩種方式可提供接聽程式設定和安全性認證：</span><span class="sxs-lookup"><span data-stu-id="f80fd-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="f80fd-115">使用 [組態封裝](service-fabric-application-model.md)提供它們：</span><span class="sxs-lookup"><span data-stu-id="f80fd-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="f80fd-116">新增`TransportSettings`hello settings.xml 檔案中的區段。</span><span class="sxs-lookup"><span data-stu-id="f80fd-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       <span data-ttu-id="f80fd-117">在此情況下，hello`createServiceInstanceListeners`方法看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f80fd-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="f80fd-118">如果您將加入`TransportSettings`沒有任何前置詞，hello settings.xml 檔案中的區段`FabricTransportListenerSettings`會從本節載入所有 hello 設定預設。</span><span class="sxs-lookup"><span data-stu-id="f80fd-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="f80fd-119">在此情況下，hello`CreateServiceInstanceListeners`方法看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f80fd-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="f80fd-120">當您呼叫方法的安全服務上使用 hello 遠端處理堆疊，而不是使用 hello`microsoft.serviceFabric.services.remoting.client.ServiceProxyBase`類別 toocreate 服務 proxy，使用`microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`。</span><span class="sxs-lookup"><span data-stu-id="f80fd-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="f80fd-121">如果 hello 用戶端程式碼做為服務一部分執行，您可以載入`FabricTransportSettings`hello settings.xml 檔案中。</span><span class="sxs-lookup"><span data-stu-id="f80fd-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="f80fd-122">建立 TransportSettings 區段是類似的 toohello 服務程式碼，如先前所示。</span><span class="sxs-lookup"><span data-stu-id="f80fd-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="f80fd-123">進行下列變更 toohello 用戶端程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="f80fd-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
