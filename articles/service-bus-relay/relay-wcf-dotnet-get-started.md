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
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Toouse Azure 轉送 WCF 如何搭配.NET 轉送
本文說明如何 toouse hello Azure 轉送服務。 hello 範例以 C# 撰寫，並使用與 hello 服務匯流排組件中所包含的延伸模組的 hello Windows Communication Foundation (WCF) 應用程式開發介面。 如需有關 Azure 轉送的詳細資訊，請參閱 hello [Azure 轉送概觀](relay-what-is-it.md)。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>什麼是 WCF 轉送？

hello Azure [ *WCF 轉送*](relay-what-is-it.md)服務可讓您在 Azure 資料中心和您自己的內部部署企業環境中執行的 toobuild 混合式應用程式。 hello 轉送服務可方便您這讓您 toosecurely 公開位於公司的企業網路 toohello 公用雲端，而不需不必 tooopen 防火牆連線，或需要的 Windows Communication Foundation (WCF) 服務具侵入性變更 tooa 公司網路基礎結構。

![WCF 轉送概念](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Azure 轉送可讓您在現有的企業環境內 toohost WCF 服務。 然後，您可以委派接聽內送工作階段與要求 toothese WCF 服務 toohello 轉送服務在 Azure 中執行。 這可讓您 tooexpose Azure，或 toomobile 工作者或夥伴外部網路環境中執行這些服務 tooapplication 程式碼。 轉送可讓您 toosecurely 控制可以存取這些服務在細微的層級。 它提供了功能強大且安全的方式 tooexpose 應用程式的功能和資料從您現有的企業解決方案和利用它從 hello 雲端。

本文將討論如何 toouse Azure 轉送 toocreate WCF web 服務，公開使用的 TCP 通道繫結，會實作兩個合作對象之間的安全對話。

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>取得 hello 服務匯流排 NuGet 封裝
hello[服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)是最簡單方式 tooget hello hello 服務匯流排 API 和 tooconfigure hello 服務匯流排相依性的所有應用程式。 tooinstall hello NuGet 封裝在專案中，請勿 hello 遵循：

1. 在 [方案總管] 中，以滑鼠右鍵按一下 [參考]，然後按一下 [管理 NuGet 套件]。
2. 搜尋 「 Service Bus 」 和選取 hello **Microsoft Azure 服務匯流排**項目。 按一下**安裝**toocomplete hello 安裝，然後關閉 hello 下列對話方塊：
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>透過 TCP 公開及取用 SOAP Web 服務
tooexpose 供外部使用現有的 WCF SOAP web 服務，您必須先變更 toohello 服務繫結和位址。 這可能需要變更 tooyour 組態檔，或可能需要變更程式碼，根據您如何設定並設定您的 WCF 服務。 請注意，WCF 可讓您 toohave 透過多個網路端點 hello 相同的服務，以便您可以保留現有的 hello 時加入外部的轉送端點的內部端點在存取 hello 相同的時間。

在這個工作中，您會建置一個簡單的 WCF 服務，並加入轉送接聽程式 tooit。 此練習中假設疐裾 Visual Studio 中，並因此不會不逐步完成建立專案的所有 hello 詳細資料。 相反地，它著重在 hello 程式碼。

開始之前這些步驟，完成下列程序 tooset 環境的 hello:

1. 在 Visual Studio 中，建立包含兩個專案，「 用戶端 」 和 「 服務 」，hello 方案中的主控台應用程式。
2. 將 hello 服務匯流排 NuGet 封裝 tooboth 專案。 此套件會將所有的 hello 必要的組件參考 tooyour 專案。

### <a name="how-toocreate-hello-service"></a>如何 toocreate hello 服務
首先，建立 hello 服務本身。 任何 WCF 服務都包含至少三個獨特部分：

* 描述何種訊息交換，以及哪些作業會叫用 toobe 合約的定義。
* 該合約的實作。
* 裝載 hello WCF 服務，而且會公開數個端點的主機。

本節中的 hello 程式碼範例可解決每個元件。

hello 合約會定義可以在單一作業`AddNumbers`，以兩個數字相加並 hello 結果。 hello`IProblemSolverChannel`介面可讓 hello 用戶端 toomore 輕鬆地管理 hello proxy 存留期。 建立此類介面被視為是最佳做法。 它是個不錯的主意 tooput 這個合約定義到個別的檔案，以便您可以從您的 「 用戶端 」 和 「 服務 」 專案中，參考該檔案，不過您也可以複製 hello 程式碼分成兩個專案。

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

就地 hello 合約，與 hello 實作如下所示：

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>以程式設計方式設定服務主機
與 hello 合約與實作中的位置，您現在可以主控 hello 服務。 主控內發生[system.servicemodel.servicehost 內](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx)物件，它會負責管理 hello 服務的執行個體，並將主機 hello 接聽訊息的端點。 hello 下列程式碼會設定 hello 服務與一般的本機端點和轉送端點 tooillustrate hello 外觀，並排的內部與外部端點。 取代字串 hello*命名空間*與命名空間名稱和*yourKey*與 hello hello 先前的安裝步驟中取得的 SAS 金鑰。

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

在 hello 範例中，您會建立兩個端點上 hello 相同的合約實作。 一個位於本機，一個透過 Azure 轉送投射。 hello 兩者之間的主要差異是 hello 繫結。[NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) hello 本機和[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) hello 轉送端點和 hello 位址。 hello 本機端點都有不同的連接埠與本機網路位址。 hello 轉送端點都有端點位址所組成的字串 hello `sb`，您的命名空間名稱和 hello 路徑 」 規劃求解。 」 這會導致 hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`，做為服務匯流排 （轉送） TCP 端點識別 hello 服務端點，具有完整的外部 DNS 名稱。 如果您 hello 將程式碼放 hello 預留位置取代成 hello`Main`函式的 hello**服務**應用程式中，您必須可運作的服務。 如果您希望您的服務 toolisten 專門針對 hello 轉送，請移除 hello 本機端點宣告。

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>在 hello App.config 檔案中設定服務主機
您也可以設定使用 hello App.config 檔案中的 hello 主機。 在此情況下裝載程式碼的 hello 服務會出現在 hello 下一個範例。

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

hello 端點定義移到 hello App.config 檔案。 hello NuGet 封裝已加入範圍定義 toohello App.config 檔案中，這是 Azure 轉送的所需的 hello 設定延伸。 下列範例中，這是精確的 hello hello hello 先前程式碼的對等項目應該會出現下方 hello **system.serviceModel**項目。 這個程式碼範例假設您的專案 C# 命名空間名稱為 **Service**。
Hello 預留位置取代您轉送命名空間名稱和 SAS 金鑰。

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

Hello 服務進行這些變更之後，啟動之前，一樣，但具有兩個即時端點： 一個本機和一個接聽 hello 雲端中。

### <a name="create-hello-client"></a>建立 hello 用戶端
#### <a name="configure-a-client-programmatically"></a>以程式設計方式設定用戶端
tooconsume hello 服務，您可以建構 WCF 用戶端使用[ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx)物件。 服務匯流排會使用以 SAS 所實作的權杖型安全性模型。 hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider)類別代表與內建的 factory 方法傳回某些已知權杖提供者的安全性權杖提供者。 hello 下列範例會使用 hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_)方法 toohandle hello 取得 hello 適當的 SAS 權杖。 hello 名稱與金鑰是取自 hello 上一節中所述的 hello 入口網站。

第一個、 參考或複製 hello`IProblemSolver`合約程式碼從 hello 服務到用戶端專案。

然後，取代 hello hello 中的程式碼`Main`hello 用戶端再次 hello 預留位置文字取代為您的轉送命名空間和 SAS 金鑰的方法。

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

您現在可以建置 hello 用戶端與 hello 服務，執行它們 （服務上執行 hello 第一次），而 hello 用戶端呼叫 hello 服務，並會列印**9**。 您可以在不同的電腦上執行 hello 用戶端和伺服器，即使是跨網路和 hello 通訊也還能運作。 在 hello 雲端或在本機，也可以執行 hello 用戶端程式碼。

#### <a name="configure-a-client-in-hello-appconfig-file"></a>設定用戶端 hello App.config 檔案中
hello，下列程式碼示範如何使用 tooconfigure hello 用戶端 hello App.config 檔案。

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

hello 端點定義移到 hello App.config 檔案。 hello 下列範例中，為 hello 與 hello 先前列出的程式碼相同，應該會出現下方 hello`<system.serviceModel>`項目。 在這裡，如往常一般，將必須 hello 預留位置取代為您的轉送命名空間和 SAS 金鑰。

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

## <a name="next-steps"></a>後續步驟
現在，您學到的 Azure 轉送的 hello 基本概念，請遵循這些連結 toolearn 更多。

* [什麼是 Azure 轉送？](relay-what-is-it.md)
* [Azure 服務匯流排架構概觀](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* 下載服務匯流排範例從[Azure 範例][ Azure samples]或參閱 hello[的服務匯流排範例概觀][overview of Service Bus samples]。

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
