---
title: "協助保護 Azure Service Fabric 中服務的通訊安全 | Microsoft Docs"
description: "如何協助保護於 Azure Service Fabric 叢集中所執行之可靠服務的通訊安全概觀。"
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
ms.openlocfilehash: c4634e3d8efb1745fffcfe3e647e43d867038716
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="3e669-103">協助保護 Azure Service Fabric 中服務的通訊安全</span><span class="sxs-lookup"><span data-stu-id="3e669-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e669-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="3e669-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="3e669-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="3e669-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="3e669-106">協助保護使用服務遠端處理時的服務安全</span><span class="sxs-lookup"><span data-stu-id="3e669-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="3e669-107">我們將使用現有 [範例](service-fabric-reliable-services-communication-remoting-java.md) 以說明如何設定可靠服務的遠端處理功能。</span><span class="sxs-lookup"><span data-stu-id="3e669-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="3e669-108">若要協助保護使用服務遠端處理時的服務安全，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="3e669-108">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="3e669-109">建立 `HelloWorldStateless`介面，這個介面會定義將在您的服務上用於遠端程序呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="3e669-109">Create an interface, `HelloWorldStateless`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="3e669-110">您的服務將使用在 `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` 封裝中宣告的 `FabricTransportServiceRemotingListener`。</span><span class="sxs-lookup"><span data-stu-id="3e669-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="3e669-111">這是提供遠端功能的 `CommunicationListener` 實作。</span><span class="sxs-lookup"><span data-stu-id="3e669-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="3e669-112">新增接聽程式設定和安全性認證。</span><span class="sxs-lookup"><span data-stu-id="3e669-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="3e669-113">確定您想要用來協助保護服務通訊安全的憑證已安裝在叢集的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="3e669-113">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="3e669-114">有兩種方式可提供接聽程式設定和安全性認證：</span><span class="sxs-lookup"><span data-stu-id="3e669-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="3e669-115">使用 [組態封裝](service-fabric-application-model.md)提供它們：</span><span class="sxs-lookup"><span data-stu-id="3e669-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="3e669-116">在 settings.xml 檔案中新增 `TransportSettings` 區段。</span><span class="sxs-lookup"><span data-stu-id="3e669-116">Add a `TransportSettings` section in the settings.xml file.</span></span>

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

       <span data-ttu-id="3e669-117">在此情況下， `createServiceInstanceListeners` 方法看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="3e669-117">In this case, the `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="3e669-118">如果您在 settings.xml 檔案中新增 `TransportSettings` 區段，而沒有任何前置詞，則 `FabricTransportListenerSettings` 預設會載入此區段中的所有設定。</span><span class="sxs-lookup"><span data-stu-id="3e669-118">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="3e669-119">在此情況下， `CreateServiceInstanceListeners` 方法看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="3e669-119">In this case, the `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="3e669-120">如果在安全服務上使用遠端堆疊來呼叫方法，而不是使用 `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 類別來建立服務 Proxy，請使用 `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`。</span><span class="sxs-lookup"><span data-stu-id="3e669-120">When you call methods on a secured service by using the remoting stack, instead of using the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class to create a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="3e669-121">如果用戶端程式碼正在當作服務一部分執行，則可以從 settings.xml 檔案中載入 `FabricTransportSettings` 。</span><span class="sxs-lookup"><span data-stu-id="3e669-121">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span></span> <span data-ttu-id="3e669-122">建立與服務程式碼類似的 TransportSettings 區段，如前所示。</span><span class="sxs-lookup"><span data-stu-id="3e669-122">Create a TransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="3e669-123">對用戶端程式碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="3e669-123">Make the following changes to the client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
