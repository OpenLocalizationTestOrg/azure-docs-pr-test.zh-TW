---
title: "教學課程中的服務匯流排的 WCF 轉送 aaaAzure |Microsoft 文件"
description: "使用 WCF 轉送來建置服務匯流排用戶端應用程式與服務。"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Azure WCF 轉送教學課程

本教學課程將告訴您如何 toobuild 簡單的 WCF 轉送用戶端應用程式和使用 Azure 轉送服務。 如需使用[服務匯流排通訊](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)的類似教學課程，請參閱[開始使用服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。

在本教學課程的工作可讓您了解必要的 toocreate 的 WCF 轉送的用戶端和服務應用程式的 hello 步驟。 如同他們原始的 WCF 對應項目，服務是可公開一或多個端點的結構，而每個端點都會公開一或多個服務作業。 hello 的服務端點指定 hello 服務可以找到的位址的繫結，其中包含用戶端必須與 hello 服務，以及定義 hello 服務 tooits 用戶端所提供的 hello 功能的合約進行通訊的 hello 資訊。 hello WCF 和 WCF 轉送之間的主要差異在於該 hello 端點會公開 hello 定域機組中而不是在本機電腦上。

Hello 系列主題逐步在本教學課程之後，您必須執行中的服務和用戶端可叫用 hello hello 服務作業。 hello 第一個主題說明如何設定帳戶 tooset。 hello 接下來的步驟說明如何 toodefine 服務使用的合約、 如何 tooimplement hello 服務，以及如何 tooconfigure hello 程式碼中的服務。 這些主題亦說明如何 toohost 和執行 hello 服務。 hello 建立的服務是自我裝載且 hello 用戶端和服務上執行 hello 同一部電腦。 您可以使用程式碼或組態檔設定 hello 服務。

hello 最後三個步驟說明 toocreate 用戶端應用程式中，設定 hello 用戶端應用程式，並建立和使用用戶端可以存取的 hello 主機 hello 功能的方式。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程中，您必須遵循的 hello:

* [Microsoft Visual Studio 2015 或更高版本](http://visualstudio.com)。 本教學課程使用 Visual Studio 2017。
* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/)。

## <a name="create-a-service-namespace"></a>建立服務命名空間

hello 第一個步驟是 toocreate 命名空間和 tooobtain[共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md)索引鍵。 命名空間提供透過 hello 轉送服務公開的每個應用程式的應用程式界限。 當建立服務命名空間 SAS 金鑰會自動產生 hello 系統。 服務命名空間和 SAS 金鑰 hello 結合 Azure tooauthenticate 存取 tooan 應用程式提供 hello 認證。 請遵循 hello[這裡的指示](relay-create-namespace-portal.md)toocreate 轉送命名空間。

## <a name="define-a-wcf-service-contract"></a>定義 WCF 服務合約

hello 服務合約會指定哪些作業 （hello web 服務術語方法或函式） hello 服務支援。 合約可以透過定義 C++、C# 或 Visual Basic 介面建立。 Hello 介面中的每個方法對應 tooa 特定服務作業。 每個介面必須有 hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)屬性套用 tooit，而且每個作業都必須有 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit 套用的屬性。 如果其中有 hello 的介面中的方法[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)屬性並沒有 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx)屬性未公開該方法。 hello 範例 hello 程序中提供這些工作的 「 hello 」 程式碼。 較大的合約和服務討論，請參閱[設計與實作服務](https://msdn.microsoft.com/library/ms729746.aspx)hello WCF 文件中。

### <a name="create-a-relay-contract-with-an-interface"></a>使用介面建立轉送合約

1. 系統管理員身分開啟 Visual Studio，以滑鼠右鍵按一下 [hello] 瀅蒰 hello**啟動**功能表，然後選取**系統管理員身分執行**。
2. 這會建立新的主控台應用程式專案。 按一下 hello**檔案**功能表，然後選取**新增**，然後按一下**專案**。 在 hello**新專案** 對話方塊中，按一下  **Visual C#** (如果**Visual C#**未出現，請查看 **其他語言**)。 按一下 hello**主控台應用程式 (.NET Framework)**範本，並將其命名**EchoService**。 按一下**確定**toocreate hello 專案。

    ![][2]

3. 安裝 hello 服務匯流排 NuGet 封裝。 此套件會自動將參考 toohello 服務匯流排程式庫，以及 hello WCF **System.ServiceModel**。 [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx)是 hello 命名空間，可讓您的 WCF 的 tooprogrammatically 存取 hello 基本功能。 服務匯流排會使用許多 hello 物件和屬性的 toodefine WCF 服務合約。

    在 方案總管 hello 專案上按一下滑鼠右鍵，然後按一下**管理 NuGet 封裝...**.按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。 確定該 hello 專案名稱已在 hello 選取**版本**方塊。 按一下**安裝**，並接受使用規定 hello。

    ![][3]
4. 在 [方案總管] 中，按兩下 hello Program.cs 檔案 tooopen 它在 hello 編輯器中，如果它尚未開啟。
5. 新增 hello 下列 using 陳述式在 hello hello 檔案最上方：

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. 中的預設名稱變更 hello 命名空間名稱**EchoService**太**Microsoft.ServiceBus.Samples**。

   > [!IMPORTANT]
   > 本教學課程使用 hello C# 命名空間**Microsoft.ServiceBus.Samples**，這是 hello 命名空間的合約為基礎的 hello managed hello 中的 hello 設定檔中所使用的型別[設定 hello WCF 用戶端](#configure-the-wcf-client)步驟。 您可以指定當您建置這個範例中，任何命名的空間不過，hello 教學課程將無法運作，除非您修改 hello hello 合約和服務的命名空間，hello 應用程式組態檔中。 hello 命名空間中 hello App.config 檔案必須指定 hello 相同 hello C# 檔案中指定的命名空間。
   >
   >
7. 直接在 hello 之後`Microsoft.ServiceBus.Samples`命名空間宣告，但 hello 命名空間中定義名為的新介面`IEchoContract`並套用 hello`ServiceContractAttribute`屬性 toohello 介面的命名空間值`http://samples.microsoft.com/ServiceModel/Relay/`。 hello 命名空間值不同於您在整個 hello 程式碼範圍內使用的 hello 命名空間。 相反地，hello 命名空間值會當做此合約唯一識別項。 明確指定 hello 命名空間，可防止 hello 預設命名空間值加入 toohello 合約名稱。 貼上下列程式碼 hello 命名空間宣告之後的 hello:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > 一般而言，hello 服務合約命名空間包含的命名配置，包括版本資訊。 Hello 服務合約命名空間中包括版本資訊可以定義新的服務合約與新的命名空間，並將新的端點上公開的服務 tooisolate 主要變更。 這種方式，用戶端可以繼續 toouse hello 舊服務合約，而不需要 toobe 更新。 版本資訊可以包含日期或組建編號。 如需詳細資訊，請參閱[服務版本設定](http://go.microsoft.com/fwlink/?LinkID=180498)。 基於 hello 本教學課程，hello 命名 hello 服務合約命名空間的結構描述不包含版本資訊。
   >
   >
8. Hello 內`IEchoContract`介面，請宣告 hello 單一作業 hello 方法`IEchoContract`hello 中的合約公開介面，並套用 hello`OperationContractAttribute`屬性 toohello 方法要做為一部分 tooexpose hello 公開的 WCF 轉送合約，如下所示：

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. 直接在 hello 之後`IEchoContract`介面定義中，宣告同時繼承自通道`IEchoContract`和也 toohello`IClientChannel`介面，如下所示：

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    通道是 hello 主機和用戶端用來傳遞資訊 tooeach 其他 hello WCF 物件。 稍後，您將撰寫 hello 通道 tooecho 資訊 hello 兩個應用程式之間的程式碼。
10. 從 hello**建置**功能表上，按一下 **建置方案**或按**Ctrl + Shift + B** tooconfirm hello 精確度的工作為止。

### <a name="example"></a>範例

下列程式碼的 hello 顯示定義的 WCF 轉送合約的基本介面。

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Hello 已建立介面，您可以實作 hello 介面。

## <a name="implement-hello-wcf-contract"></a>實作 hello WCF 合約

建立 Azure 的轉送，您必須先建立 hello 合約，它使用介面所定義。 如需有關建立 hello 介面的詳細資訊，請參閱 hello 上一個步驟。 hello 下一個步驟是 tooimplement hello 介面。 這項作業包括建立類別，名為`EchoService`實作使用者定義的 hello`IEchoContract`介面。 實作 hello 介面之後，接著您設定 hello 介面使用 App.config 組態檔。 hello 設定檔包含 hello 應用程式，例如 hello hello 服務名稱、 hello 名稱 hello 合約和通訊協定都使用的 toocommunicate 與 hello 轉送服務的 hello 類型的必要資訊。 hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。 如需如何 tooimplement 服務合約的一般討論，請參閱[實作服務合約](https://msdn.microsoft.com/library/ms733764.aspx)hello WCF 文件中。

1. 建立新的類別，名為`EchoService`的 hello 的 hello 定義之後，直接`IEchoContract`介面。 hello`EchoService`類別會實作 hello`IEchoContract`介面。

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    類似 tooother 介面實作，您可以實作 hello 定義不同的檔案中。 不過，本教學課程，hello 實作位於相同檔案做為 hello 介面定義，hello hello`Main`方法。
2. 套用 hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx)屬性 toohello`IEchoContract`介面。 hello 屬性會指定 hello 服務名稱和命名空間。 之後，請 hello`EchoService`類別會出現，如下所示：

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. 實作 hello`Echo`方法定義於 hello`IEchoContract`介面中 hello`EchoService`類別。

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. 按一下**建置**，然後按一下 **建置方案**tooconfirm hello 精確度的工作。

### <a name="define-hello-configuration-for-hello-service-host"></a>定義 hello hello 服務主機的組態

1. hello 組態檔是非常類似 tooa WCF 組態檔。 它包含 hello 服務名稱、 端點 （也就是 hello 位置 Azure 轉送會公開為用戶端和主機彼此 toocommunicate），並 hello 繫結 （通訊協定都使用的 toocommunicate hello 類型）。 hello 主要差異在於此設定的服務端點會參考 tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding)繫結，這不是 hello.NET Framework 的一部分。 [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding)是其中一個 hello hello 服務所定義的繫結。
2. 在**方案總管 中**，按兩下 hello App.config 檔案 tooopen hello Visual Studio 編輯器中。
3. 在 hello `<appSettings>` hello 預留位置取代為您的服務命名空間中的 hello 名稱項目，和 hello 您在前述步驟中複製的 SAS 金鑰。
4. Hello 內`<system.serviceModel>`標記，加入`<services>`項目。 您可以在單一組態檔中定義多個轉送應用程式。 不過，本教學課程只會定義一個。

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. 在 hello`<services>`項目，加入`<service>`hello 服務項目 toodefine hello 名稱。

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. 在 hello`<service>`項目，定義 hello 位置 hello 端點合約，並也 hello hello 端點的繫結型別。

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    hello 端點定義 hello 用戶端將在其中尋找 hello 主應用程式。 稍後，hello 教學課程會使用此步驟 toocreate 完全公開透過 Azure 轉送 hello 主機的 URI。 hello 繫結宣告我們使用 TCP hello 與 hello 轉送服務的通訊協定 toocommunicate 如下。
7. 從 hello**建置**功能表上，按一下 **建置方案**tooconfirm hello 精確度的工作。

### <a name="example"></a>範例

hello 下列程式碼顯示 hello hello 服務合約實作。

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

hello 下列程式碼顯示 hello hello 與 hello 服務主機相關聯的 App.config 檔案的基本格式。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>裝載和執行基本 web 服務 tooregister 與 hello 轉送服務

此步驟說明如何 toorun Azure 轉送服務。

### <a name="create-hello-relay-credentials"></a>建立 hello 轉送認證

1. 在`Main()`、 哪些 toostore hello 命名空間中建立兩個變數和 hello 從 hello 主控台視窗讀取的 SAS 金鑰。

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    hello SAS 金鑰將會使用更新版本的 tooaccess 您的專案。 hello 命名空間會當做參數傳遞太`CreateServiceUri`toocreate 服務 URI。
2. 使用[TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior)物件，宣告您將使用 SAS 金鑰作為 hello 認證類型。 新增下列程式碼直接在 hello hello 最後一個步驟中加入的程式碼之後的 hello。

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>建立 hello 服務的基底地址

Hello hello 最後一個步驟中加入程式碼之後, 建立`Uri`hello 基底地址的 hello 服務的執行個體。 此 URI 指定 hello Service Bus 配置、 hello 命名空間及 hello 路徑 hello 服務介面。

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

「 sb 」 hello Service Bus 配置的縮寫，表示我們使用 TCP 做為 hello 通訊協定。 這也先前已指出 hello 組態檔中，當[NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx)被指定為 hello 繫結。

此教學課程，hello URI 是`sb://putServiceNamespaceHere.windows.net/EchoService`。

### <a name="create-and-configure-hello-service-host"></a>建立及設定 hello 服務主機

1. Hello 連線模式設定太`AutoDetect`。

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    hello 連線模式可描述 hello 通訊協定 hello 服務會使用 toocommunicate 與 hello 轉送服務。HTTP 或 TCP。 使用 hello 預設設定`AutoDetect`，hello 服務會嘗試透過 TCP，如果有的話和 HTTP tooconnect tooAzure 轉送如果無法使用 TCP。 請注意，這不同於 hello 通訊協定 hello 服務指定用戶端通訊。 使用 hello 繫結會判斷該通訊協定。 例如，服務可以使用 hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx)繫結，這會指定，其端點與用戶端透過 HTTP 進行通訊。 相同服務可以指定**ConnectivityMode.AutoDetect**以便 hello 服務與 Azure 轉送透過 TCP 通訊。
2. 建立 hello 服務主機，請使用本節稍早建立 URI 的 hello。

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    具現化 hello 服務的 hello WCF 物件 hello 服務主機。 在這裡，您將它傳遞 hello 類型的服務，您想 toocreate (`EchoService`類型)，和也想 tooexpose hello 服務 toohello 位址。
3. 在 hello hello Program.cs 檔案頂端，加入參考太[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx)和[Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description)。

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. 回到`Main()`，設定 hello 端點 tooenable 公用存取。

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    此步驟會通知 hello 轉送服務，您的應用程式即可公開找到藉由檢查專案的 hello ATOM 摘要。 如果您設定**DiscoveryType**太**私人**，用戶端仍將是無法 tooaccess hello 服務。 不過，hello 服務不會出現搜尋 hello 轉送命名空間時。 相反地，hello 用戶端會事先有 tooknow hello 端點路徑。
5. 套用 hello 服務認證 toohello hello App.config 檔案中定義的服務端點：

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Hello 上一個步驟所述，您無法宣告多個服務和 hello 組態檔中的端點。 如果您在這段程式碼會周遊 hello 組態檔案，並搜尋針對每個端點 toowhich 應套用您的認證。 不過，本教學課程，hello 設定檔有只有一個端點。

### <a name="open-hello-service-host"></a>開啟 hello 服務主機

1. 開啟 hello 服務。

    ```csharp
    host.Open();
    ```
2. 通知 hello 服務的 hello 使用者執行，並且說明如何關閉 hello 服務 tooshut。

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. 完成後，關閉 hello 服務主機。

    ```csharp
    host.Close();
    ```
4. 按**Ctrl + Shift + B** toobuild hello 專案。

### <a name="example"></a>範例

完整的服務程式碼應如下所示。 hello 程式碼包含 hello 服務合約和實作，從上一個步驟中 hello 教學課程中，並裝載 hello 主控台應用程式中的服務。

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>建立 hello 服務合約的 WCF 用戶端

hello 下一個步驟是 toocreate 用戶端應用程式，並定義 hello 服務合約，您將在稍後步驟中實作。 請注意，其中許多步驟類似於 hello 步驟使用 toocreate 服務： 定義合約、 編輯 App.config 檔案，使用認證 tooconnect toohello 轉送服務，以此類推。 hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。

1. 執行下列 hello hello 用戶端 hello 目前 Visual Studio 方案中建立新的專案：

   1. 在 方案總管在 hello 相同的方案，其中包含 hello 服務，hello 目前的方案 （不 hello 專案），以滑鼠右鍵按一下，按一下 **新增**。 然後按一下新增專案。
   2. 在 hello**加入新的專案**對話方塊中，按一下  **Visual C#** (如果**Visual C#**未出現，請查看 **其他語言**)，請選取 hello**主控台應用程式 (.NET Framework)**範本，並將其命名**EchoClient**。
   3. 按一下 [確定] 。
      <br />
2. 在 [方案總管] 中，按兩下 hello Program.cs 檔案中 hello **EchoClient** tooopen 它在 hello 編輯器中，如果還沒有開啟的專案。
3. 中的預設名稱變更 hello 命名空間名稱`EchoClient`太`Microsoft.ServiceBus.Samples`。
4. 安裝 hello[服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)： 在方案總管 中，以滑鼠右鍵按一下 hello **EchoClient**專案，然後再按一下**管理 NuGet 封裝**。 按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。 按一下**安裝**，並接受使用規定 hello。

    ![][3]
5. 新增`using`hello 陳述式[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello Program.cs 檔案中的命名空間。

    ```csharp
    using System.ServiceModel;
    ```
6. 加入 hello 服務合約定義 toohello 命名空間，hello 下列範例所示。 請注意，這個定義是相同的 toohello 定義用於 hello**服務**專案。 您應該在 hello hello 最上方加入下列程式碼`Microsoft.ServiceBus.Samples`命名空間。

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. 按**Ctrl + Shift + B** toobuild hello 用戶端。

### <a name="example"></a>範例

hello 下列程式碼顯示 hello 目前狀態的 hello Program.cs 檔案中 hello **EchoClient**專案。

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Hello WCF 用戶端設定

在此步驟中，您可以建立的 App.config 檔案，存取先前在本教學課程中建立的 hello 服務的基本用戶端應用程式。 此 App.config 檔案定義 hello 合約、 繫結和 hello 端點的名稱。 hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。

1. 在 方案總管中 hello **EchoClient**專案中，按兩下**App.config** tooopen hello Visual Studio 編輯器中的 hello 檔案。
2. 在 hello `<appSettings>` hello 預留位置取代為您的服務命名空間中的 hello 名稱項目，和 hello 您在前述步驟中複製的 SAS 金鑰。
3. 在 hello system.serviceModel 項目，將新增`<client>`項目。

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    此步驟宣告您正在定義 WCF 樣式的用戶端應用程式。
4. 在 hello`client`項目，定義 hello 名稱、 合約和 hello 端點的繫結型別。

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    此步驟定義 hello hello 端點，且定義為 hello 服務和 hello 事實 hello 用戶端應用程式會使用與 Azure 轉送 TCP toocommunicate hello 合約名稱。 hello 端點的名稱會在 hello 下一步 toolink hello 服務 URI 與此端點組態。
5. 按一下 [檔案]，然後按一下 [全部儲存]。

## <a name="example"></a>範例

hello 下列程式碼顯示 hello hello Echo 用戶端的 App.config 檔案。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>實作 hello WCF 用戶端
在此步驟中，您可以實作基本用戶端應用程式存取您先前在本教學課程中建立的 hello 服務。 Hello 用戶端執行許多 hello 類似 toohello 服務時，相同作業 tooaccess Azure 轉送：

1. 設定 hello 連線模式。
2. 建立 hello 找出 hello 主機服務的 URI。
3. 定義 hello 安全性認證。
4. 適用於 hello 認證 toohello 連接。
5. 開啟 hello 連線。
6. 執行 hello 應用程式特定的工作。
7. 關閉 hello 連接。

不過，其中一個 hello 主要差異是 hello 用戶端應用程式會使用通道 tooconnect toohello 轉送服務，而 hello 服務會使用呼叫太**ServiceHost**。 hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。

### <a name="implement-a-client-application"></a>實作用戶端應用程式
1. Hello 連線模式設定太**自動偵測**。 新增下列程式碼內 hello hello`Main()`方法 hello **EchoClient**應用程式。

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. 定義變數 toohold hello hello 服務命名空間，以及 SAS 金鑰的值從 hello 主控台讀取的。

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. 建立 hello 轉送專案中定義的 hello 主機的 hello 位置的 URI。

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. 建立服務命名空間端點 hello 認證物件。

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. 建立 hello 通道處理站載入 hello hello App.config 檔案中所述的組態。

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    通道處理站會建立的通道，透過此 hello 服務與用戶端應用程式進行通訊的 WCF 物件。
6. 套用 hello 認證。

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. 建立並開啟 hello 通道 toohello 服務。

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. 撰寫 hello 基本使用者介面與 hello 回應的功能。

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    請注意，hello 程式碼使用 hello hello 通道物件執行個體做為 proxy hello 服務。
9. 關閉 hello 通道和關閉 hello factory。

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>範例

您已完成的程式碼應該會出現，如下所示，顯示如何 toocreate 用戶端應用程式、 toocall hello hello 服務作業的方式和 tooclose hello 作業之後所 hello 的用戶端呼叫已完成。

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>執行 hello 應用程式

1. 按**Ctrl + Shift + B** toobuild hello 方案。 這會建置 hello 用戶端專案和 hello hello 先前步驟中建立的服務專案。
2. 之前執行的 hello 用戶端應用程式，您必須確定 hello 服務應用程式正在執行。 在 Visual Studio 中的方案總管] 中以滑鼠右鍵按一下 hello **EchoService**方案，然後按一下 [**屬性**。
3. 在 [hello 方案內容] 對話方塊中按一下**啟始專案**，然後按一下 [hello**多個啟始專案**] 按鈕。 請確定**EchoService** hello 清單中第一個出現。
4. 設定 hello**動作**方塊這兩個 hello **EchoService**和**EchoClient**太專案**啟動**。

    ![][5]
5. 按一下 [專案相依性]。 在 hello**專案**方塊中，選取**EchoClient**。 在 hello**取決於**方塊中，請確定**EchoService**已核取。

    ![][6]
6. 按一下**確定**toodismiss hello**屬性**對話方塊。
7. 按**F5** toorun 這兩個專案。
8. 兩個主控台視窗開啟，並提示您輸入 hello 命名空間名稱。 hello 服務必須先執行，所以在 hello **EchoService**主控台視窗中，輸入 hello 命名空間，然後按**Enter**。
9. 接下來，系統會提示您輸入 SAS 金鑰。 輸入 hello SAS 金鑰，然後按 ENTER。

    以下是 hello 主控台視窗的輸出範例。 請注意以下是僅限用途，例如提供 hello 值。

    `Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`

    hello 服務應用程式列印 toohello 主控台視窗 hello 它會接聽的位址，如 hello 下列範例所示。

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`
10. 在 hello **EchoClient**主控台視窗中，輸入 hello hello 服務應用程式先前輸入的相同資訊。 請依照上一個步驟 tooenter hello hello 相同的服務命名空間和 SAS 金鑰 hello 用戶端應用程式的值。
11. 輸入這些值之後, hello 用戶端通道 toohello 服務就會開啟，並提示您 tooenter 一些文字，如 hello 下列主控台輸出範例所示。

    `Enter text tooecho (or [Enter] tooexit):`

    輸入一些文字 toosend toohello 服務應用程式，然後按 Enter。 此文字會傳送 toohello 服務透過 hello Echo 服務作業，並會出現在 hello 服務主控台視窗，如下列範例輸出的 hello 所示。

    `Echoing: My sample text`

    hello 用戶端應用程式收到 hello 傳回值的 hello`Echo`作業，因為它是原始的 hello 文字，並將它列印 tooits 主控台視窗。 hello 以下是 hello 用戶端主控台視窗的輸出範例。

    `Server echoed: My sample text`
12. 您可以繼續從這種方式中的 hello 用戶端 toohello 服務傳送文字訊息。 當您完成時，按 Enter 鍵 hello 用戶端和服務主控台視窗 tooend 中兩個應用程式。

## <a name="next-steps"></a>後續步驟

本教學課程示範了如何 toobuild Azure 轉接用戶端應用程式和服務使用 hello 的服務匯流排的 WCF 轉送功能。 如需使用[服務匯流排通訊](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)的類似教學課程，請參閱[開始使用服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。

toolearn 深入了解 Azure 轉送，請參閱下列主題中的 hello。

* [Azure 服務匯流排架構概觀](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Azure 轉送概觀](relay-what-is-it.md)
* [如何 toouse hello WCF 轉送服務的.NET](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
