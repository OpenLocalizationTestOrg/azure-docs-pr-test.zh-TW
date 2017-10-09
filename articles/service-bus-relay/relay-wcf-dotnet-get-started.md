---
title: "aaaGet 開始使用.net 的 Azure 轉送的 WCF 轉送 |Microsoft 文件"
description: "了解如何 toouse Azure 轉送的 WCF 轉送 tooconnect 兩個應用程式裝載在不同的位置。"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="2dc76-103">Toouse Azure 轉送 WCF 如何搭配.NET 轉送</span><span class="sxs-lookup"><span data-stu-id="2dc76-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="2dc76-104">本文說明如何 toouse hello Azure 轉送服務。</span><span class="sxs-lookup"><span data-stu-id="2dc76-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="2dc76-105">hello 範例以 C# 撰寫，並使用與 hello 服務匯流排組件中所包含的延伸模組的 hello Windows Communication Foundation (WCF) 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="2dc76-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="2dc76-106">如需有關 Azure 轉送的詳細資訊，請參閱 hello [Azure 轉送概觀](relay-what-is-it.md)。</span><span class="sxs-lookup"><span data-stu-id="2dc76-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="2dc76-107">什麼是 WCF 轉送？</span><span class="sxs-lookup"><span data-stu-id="2dc76-107">What is WCF Relay?</span></span>

<span data-ttu-id="2dc76-108">hello Azure [ *WCF 轉送*](relay-what-is-it.md)服務可讓您在 Azure 資料中心和您自己的內部部署企業環境中執行的 toobuild 混合式應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dc76-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="2dc76-109">hello 轉送服務可方便您這讓您 toosecurely 公開位於公司的企業網路 toohello 公用雲端，而不需不必 tooopen 防火牆連線，或需要的 Windows Communication Foundation (WCF) 服務具侵入性變更 tooa 公司網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="2dc76-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![WCF 轉送概念](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="2dc76-111">Azure 轉送可讓您在現有的企業環境內 toohost WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="2dc76-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="2dc76-112">然後，您可以委派接聽內送工作階段與要求 toothese WCF 服務 toohello 轉送服務在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="2dc76-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="2dc76-113">這可讓您 tooexpose Azure，或 toomobile 工作者或夥伴外部網路環境中執行這些服務 tooapplication 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2dc76-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="2dc76-114">轉送可讓您 toosecurely 控制可以存取這些服務在細微的層級。</span><span class="sxs-lookup"><span data-stu-id="2dc76-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="2dc76-115">它提供了功能強大且安全的方式 tooexpose 應用程式的功能和資料從您現有的企業解決方案和利用它從 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="2dc76-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="2dc76-116">本文將討論如何 toouse Azure 轉送 toocreate WCF web 服務，公開使用的 TCP 通道繫結，會實作兩個合作對象之間的安全對話。</span><span class="sxs-lookup"><span data-stu-id="2dc76-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="2dc76-117">取得 hello 服務匯流排 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="2dc76-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="2dc76-118">hello[服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)是最簡單方式 tooget hello hello 服務匯流排 API 和 tooconfigure hello 服務匯流排相依性的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dc76-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="2dc76-119">tooinstall hello NuGet 封裝在專案中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="2dc76-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="2dc76-120">在 [方案總管] 中，以滑鼠右鍵按一下 [參考]，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="2dc76-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="2dc76-121">搜尋 「 Service Bus 」 和選取 hello **Microsoft Azure 服務匯流排**項目。</span><span class="sxs-lookup"><span data-stu-id="2dc76-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="2dc76-122">按一下**安裝**toocomplete hello 安裝，然後關閉 hello 下列對話方塊：</span><span class="sxs-lookup"><span data-stu-id="2dc76-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="2dc76-123">透過 TCP 公開及取用 SOAP Web 服務</span><span class="sxs-lookup"><span data-stu-id="2dc76-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="2dc76-124">tooexpose 供外部使用現有的 WCF SOAP web 服務，您必須先變更 toohello 服務繫結和位址。</span><span class="sxs-lookup"><span data-stu-id="2dc76-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="2dc76-125">這可能需要變更 tooyour 組態檔，或可能需要變更程式碼，根據您如何設定並設定您的 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="2dc76-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="2dc76-126">請注意，WCF 可讓您 toohave 透過多個網路端點 hello 相同的服務，以便您可以保留現有的 hello 時加入外部的轉送端點的內部端點在存取 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="2dc76-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="2dc76-127">在這個工作中，您會建置一個簡單的 WCF 服務，並加入轉送接聽程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="2dc76-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="2dc76-128">此練習中假設疐裾 Visual Studio 中，並因此不會不逐步完成建立專案的所有 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2dc76-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="2dc76-129">相反地，它著重在 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2dc76-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="2dc76-130">開始之前這些步驟，完成下列程序 tooset 環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="2dc76-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="2dc76-131">在 Visual Studio 中，建立包含兩個專案，「 用戶端 」 和 「 服務 」，hello 方案中的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dc76-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="2dc76-132">將 hello 服務匯流排 NuGet 封裝 tooboth 專案。</span><span class="sxs-lookup"><span data-stu-id="2dc76-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="2dc76-133">此套件會將所有的 hello 必要的組件參考 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="2dc76-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="2dc76-134">如何 toocreate hello 服務</span><span class="sxs-lookup"><span data-stu-id="2dc76-134">How toocreate hello service</span></span>
<span data-ttu-id="2dc76-135">首先，建立 hello 服務本身。</span><span class="sxs-lookup"><span data-stu-id="2dc76-135">First, create hello service itself.</span></span> <span data-ttu-id="2dc76-136">任何 WCF 服務都包含至少三個獨特部分：</span><span class="sxs-lookup"><span data-stu-id="2dc76-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="2dc76-137">描述何種訊息交換，以及哪些作業會叫用 toobe 合約的定義。</span><span class="sxs-lookup"><span data-stu-id="2dc76-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="2dc76-138">該合約的實作。</span><span class="sxs-lookup"><span data-stu-id="2dc76-138">Implementation of that contract.</span></span>
* <span data-ttu-id="2dc76-139">裝載 hello WCF 服務，而且會公開數個端點的主機。</span><span class="sxs-lookup"><span data-stu-id="2dc76-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="2dc76-140">本節中的 hello 程式碼範例可解決每個元件。</span><span class="sxs-lookup"><span data-stu-id="2dc76-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="2dc76-141">hello 合約會定義可以在單一作業`AddNumbers`，以兩個數字相加並 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="2dc76-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="2dc76-142">hello`IProblemSolverChannel`介面可讓 hello 用戶端 toomore 輕鬆地管理 hello proxy 存留期。</span><span class="sxs-lookup"><span data-stu-id="2dc76-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="2dc76-143">建立此類介面被視為是最佳做法。</span><span class="sxs-lookup"><span data-stu-id="2dc76-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="2dc76-144">它是個不錯的主意 tooput 這個合約定義到個別的檔案，以便您可以從您的 「 用戶端 」 和 「 服務 」 專案中，參考該檔案，不過您也可以複製 hello 程式碼分成兩個專案。</span><span class="sxs-lookup"><span data-stu-id="2dc76-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

<span data-ttu-id="2dc76-145">就地 hello 合約，與 hello 實作如下所示：</span><span class="sxs-lookup"><span data-stu-id="2dc76-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="2dc76-146">以程式設計方式設定服務主機</span><span class="sxs-lookup"><span data-stu-id="2dc76-146">Configure a service host programmatically</span></span>
<span data-ttu-id="2dc76-147">與 hello 合約與實作中的位置，您現在可以主控 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="2dc76-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="2dc76-148">主控內發生[system.servicemodel.servicehost 內](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx)物件，它會負責管理 hello 服務的執行個體，並將主機 hello 接聽訊息的端點。</span><span class="sxs-lookup"><span data-stu-id="2dc76-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="2dc76-149">hello 下列程式碼會設定 hello 服務與一般的本機端點和轉送端點 tooillustrate hello 外觀，並排的內部與外部端點。</span><span class="sxs-lookup"><span data-stu-id="2dc76-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="2dc76-150">取代字串 hello*命名空間*與命名空間名稱和*yourKey*與 hello hello 先前的安裝步驟中取得的 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dc76-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="2dc76-151">在 hello 範例中，您會建立兩個端點上 hello 相同的合約實作。</span><span class="sxs-lookup"><span data-stu-id="2dc76-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="2dc76-152">一個位於本機，一個透過 Azure 轉送投射。</span><span class="sxs-lookup"><span data-stu-id="2dc76-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="2dc76-153">hello 兩者之間的主要差異是 hello 繫結。[NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) hello 本機和[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) hello 轉送端點和 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="2dc76-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="2dc76-154">hello 本機端點都有不同的連接埠與本機網路位址。</span><span class="sxs-lookup"><span data-stu-id="2dc76-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="2dc76-155">hello 轉送端點都有端點位址所組成的字串 hello `sb`，您的命名空間名稱和 hello 路徑 」 規劃求解。 」</span><span class="sxs-lookup"><span data-stu-id="2dc76-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="2dc76-156">這會導致 hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`，做為服務匯流排 （轉送） TCP 端點識別 hello 服務端點，具有完整的外部 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="2dc76-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="2dc76-157">如果您 hello 將程式碼放 hello 預留位置取代成 hello`Main`函式的 hello**服務**應用程式中，您必須可運作的服務。</span><span class="sxs-lookup"><span data-stu-id="2dc76-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="2dc76-158">如果您希望您的服務 toolisten 專門針對 hello 轉送，請移除 hello 本機端點宣告。</span><span class="sxs-lookup"><span data-stu-id="2dc76-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="2dc76-159">在 hello App.config 檔案中設定服務主機</span><span class="sxs-lookup"><span data-stu-id="2dc76-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="2dc76-160">您也可以設定使用 hello App.config 檔案中的 hello 主機。</span><span class="sxs-lookup"><span data-stu-id="2dc76-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="2dc76-161">在此情況下裝載程式碼的 hello 服務會出現在 hello 下一個範例。</span><span class="sxs-lookup"><span data-stu-id="2dc76-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="2dc76-162">hello 端點定義移到 hello App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="2dc76-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="2dc76-163">hello NuGet 封裝已加入範圍定義 toohello App.config 檔案中，這是 Azure 轉送的所需的 hello 設定延伸。</span><span class="sxs-lookup"><span data-stu-id="2dc76-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="2dc76-164">下列範例中，這是精確的 hello hello hello 先前程式碼的對等項目應該會出現下方 hello **system.serviceModel**項目。</span><span class="sxs-lookup"><span data-stu-id="2dc76-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="2dc76-165">這個程式碼範例假設您的專案 C# 命名空間名稱為 **Service**。</span><span class="sxs-lookup"><span data-stu-id="2dc76-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="2dc76-166">Hello 預留位置取代您轉送命名空間名稱和 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dc76-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

<span data-ttu-id="2dc76-167">Hello 服務進行這些變更之後，啟動之前，一樣，但具有兩個即時端點： 一個本機和一個接聽 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="2dc76-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="2dc76-168">建立 hello 用戶端</span><span class="sxs-lookup"><span data-stu-id="2dc76-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="2dc76-169">以程式設計方式設定用戶端</span><span class="sxs-lookup"><span data-stu-id="2dc76-169">Configure a client programmatically</span></span>
<span data-ttu-id="2dc76-170">tooconsume hello 服務，您可以建構 WCF 用戶端使用[ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx)物件。</span><span class="sxs-lookup"><span data-stu-id="2dc76-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="2dc76-171">服務匯流排會使用以 SAS 所實作的權杖型安全性模型。</span><span class="sxs-lookup"><span data-stu-id="2dc76-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="2dc76-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider)類別代表與內建的 factory 方法傳回某些已知權杖提供者的安全性權杖提供者。</span><span class="sxs-lookup"><span data-stu-id="2dc76-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="2dc76-173">hello 下列範例會使用 hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_)方法 toohandle hello 取得 hello 適當的 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="2dc76-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="2dc76-174">hello 名稱與金鑰是取自 hello 上一節中所述的 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2dc76-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="2dc76-175">第一個、 參考或複製 hello`IProblemSolver`合約程式碼從 hello 服務到用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="2dc76-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="2dc76-176">然後，取代 hello hello 中的程式碼`Main`hello 用戶端再次 hello 預留位置文字取代為您的轉送命名空間和 SAS 金鑰的方法。</span><span class="sxs-lookup"><span data-stu-id="2dc76-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="2dc76-177">您現在可以建置 hello 用戶端與 hello 服務，執行它們 （服務上執行 hello 第一次），而 hello 用戶端呼叫 hello 服務，並會列印**9**。</span><span class="sxs-lookup"><span data-stu-id="2dc76-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="2dc76-178">您可以在不同的電腦上執行 hello 用戶端和伺服器，即使是跨網路和 hello 通訊也還能運作。</span><span class="sxs-lookup"><span data-stu-id="2dc76-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="2dc76-179">在 hello 雲端或在本機，也可以執行 hello 用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="2dc76-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="2dc76-180">設定用戶端 hello App.config 檔案中</span><span class="sxs-lookup"><span data-stu-id="2dc76-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="2dc76-181">hello，下列程式碼示範如何使用 tooconfigure hello 用戶端 hello App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="2dc76-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="2dc76-182">hello 端點定義移到 hello App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="2dc76-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="2dc76-183">hello 下列範例中，為 hello 與 hello 先前列出的程式碼相同，應該會出現下方 hello`<system.serviceModel>`項目。</span><span class="sxs-lookup"><span data-stu-id="2dc76-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="2dc76-184">在這裡，如往常一般，將必須 hello 預留位置取代為您的轉送命名空間和 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dc76-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a><span data-ttu-id="2dc76-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2dc76-185">Next steps</span></span>
<span data-ttu-id="2dc76-186">現在，您學到的 Azure 轉送的 hello 基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="2dc76-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="2dc76-187">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="2dc76-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="2dc76-188">Azure 服務匯流排架構概觀</span><span class="sxs-lookup"><span data-stu-id="2dc76-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="2dc76-189">下載服務匯流排範例從[Azure 範例][ Azure samples]或參閱 hello[的服務匯流排範例概觀][overview of Service Bus samples]。</span><span class="sxs-lookup"><span data-stu-id="2dc76-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
