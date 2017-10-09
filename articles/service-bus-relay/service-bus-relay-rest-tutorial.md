---
title: "使用 Azure 轉送 aaaService Bus REST 教學課程 |Microsoft 文件"
description: "建置簡單的 Azure 服務匯流排轉送主機應用程式來公開 REST 架構介面。"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Azure WCF 轉送的 REST 教學課程

本教學課程說明如何 toobuild 簡單的 Azure 轉送裝載以 REST 為基礎的介面公開 （expose） 的應用程式。 其餘可讓 web 用戶端，例如網頁瀏覽器，透過 HTTP 的服務匯流排 Api 要求 tooaccess hello。

hello 教學課程會使用服務匯流排上 hello Windows Communication Foundation (WCF) REST 程式設計模型 tooconstruct REST 服務。 如需詳細資訊，請參閱[WCF REST 程式設計模型](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model)和[設計與實作服務](/dotnet/framework/wcf/designing-and-implementing-services)hello WCF 文件中。

## <a name="step-1-create-a-namespace"></a>步驟 1：建立命名空間

使用 toobegin hello 轉送功能，在 Azure 中的，您必須先建立服務命名空間。 命名空間提供範圍容器，可在應用程式內進行 Azure 資源定址。 請遵循 hello[這裡的指示](relay-create-namespace-portal.md)toocreate 轉送命名空間。

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>步驟 2： 定義與 Azure 轉送的 REST 式 WCF 服務合約 toouse

當您建立 WCF rest 服務時，您必須定義 hello 合約。 hello 合約會指定哪些作業 hello 主應用程式支援。 服務作業可視為 Web 服務方法。 合約可以透過定義 C++、C# 或 Visual Basic 介面建立。 Hello 介面中的每個方法對應 tooa 特定服務作業。 hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)屬性必須套用的 tooeach 介面和 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx)屬性必須套用的 tooeach 作業。 如果其中有 hello 的介面中的方法[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)沒有 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx)，未公開該方法。 hello 用於這些工作的程式碼所示 hello hello 程序的範例。

hello WCF 合約和 rest 式合約的主要差異是 hello 新增屬性 toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx)。 此屬性可讓 hello 介面的另一端 toomap 上 hello 介面 tooa 方法中的方法。 在此情況下，我們將使用[WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink 方法 tooHTTP GET。 這可讓服務匯流排 tooaccurately 擷取和解譯傳送 toohello 介面的命令。

### <a name="toocreate-a-contract-with-an-interface"></a>toocreate 合約的介面

1. 開啟 Visual Studio 以系統管理員： hello 中的以滑鼠右鍵按一下 hello 程式**啟動**功能表，然後再按一下**系統管理員身分執行**。
2. 這會建立新的主控台應用程式專案。 按一下 hello**檔案**功能表，然後選取**新增**，然後選取**專案**。 在 hello**新專案**對話方塊中，按一下**Visual C#**，選取 hello**主控台應用程式**範本，並將它命名**ImageListener**。 使用預設的 hello**位置**。 按一下**確定**toocreate hello 專案。
3. 若為 C# 專案，Visual Studio 會建立 `Program.cs` 檔案。 這個類別包含空`Main()`正確主控台應用程式專案 toobuild 所需的方法。
4. 新增參考 tooService 匯流排和**System.ServiceModel.dll** toohello 專案藉由安裝 hello 服務匯流排 NuGet 封裝。 此套件會自動將參考 toohello 服務匯流排程式庫，以及 hello WCF **System.ServiceModel**。 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ImageListener**專案，然後再按一下**管理 NuGet 封裝**。 按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。 按一下**安裝**，並接受使用規定 hello。
5. 您必須明確的加入的參考**System.ServiceModel.Web.dll** toohello 專案：
   
    a. 在 [方案總管] 中，以滑鼠右鍵按一下 hello**參考**下 hello 專案資料夾，然後按一下資料夾**加入參考**。
   
    b. 在 [hello**加入參考**對話方塊方塊中，按一下 hello **Framework** ] 索引標籤左側為 hello 和 hello**搜尋**方塊中，輸入**System.ServiceModel.Web**. 選取 hello **System.ServiceModel.Web**核取方塊，然後按一下 **確定**。
6. 新增下列 hello`using`在 hello hello Program.cs 檔案最上方的陳述式。
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx)是 hello 命名空間，可讓 WCF 以程式設計方式存取 toobasic 功能。 許多 hello 物件和屬性的 toodefine WCF 服務合約，則會使用 WCF 轉送。 您將在大部分轉送應用程式中使用此命名空間。 同樣地， [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx)有助於定義 hello 通道，這是您與 Azure 轉送和 hello 的用戶端 web 瀏覽器透過此通訊的 hello 物件。 最後， [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx)包含 hello toocreate web 應用程式可讓您的型別。
7. 重新命名 hello`ImageListener`命名空間太**Microsoft.ServiceBus.Samples**。
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. 直接之後 hello 開啟 hello 命名空間宣告的大括號，定義名為的新介面**IImageContract**並套用 hello **ServiceContractAttribute**屬性 toohello 介面值`http://samples.microsoft.com/ServiceModel/Relay/`。 hello 命名空間值不同於您在整個 hello 程式碼範圍內使用的 hello 命名空間。 hello 命名空間值作為此合約，唯一的識別項，且必須有版本資訊。 如需詳細資訊，請參閱[服務版本設定](http://go.microsoft.com/fwlink/?LinkID=180498)。 明確指定 hello 命名空間，可防止 hello 預設命名空間值加入 toohello 合約名稱。
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. Hello 內`IImageContract`介面，請宣告 hello 單一作業 hello 方法`IImageContract`hello 中的合約公開介面，並套用 hello`OperationContractAttribute`屬性為 hello 公開服務匯流排的一部分，想 tooexpose toohello 方法合約。
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. 在 hello **OperationContract**屬性，請將 hello **WebGet**值。
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    這麼做會讓 hello 太 HTTP GET 要求的轉送服務 tooroute`GetImage`，並傳回值的 tootranslate hello`GetImage`成 HTTP GETRESPONSE 回覆。 稍後在 hello 教學課程中，您將使用 web 瀏覽器 tooaccess 這個方法，以及 toodisplay hello 映像 hello 瀏覽器中。
11. 直接在 hello 之後`IImageContract`定義，宣告繼承自兩個 hello 通道`IImageContract`和`IClientChannel`介面。
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    通道是 hello 服務與用戶端用來傳遞資訊 tooeach 其他 hello WCF 物件。 稍後，您將建立 hello 通道在主控件應用程式。 Azure 轉送然後會使用此通道 toopass hello HTTP GET 要求從 hello 瀏覽器 tooyour **GetImage**實作。 hello 轉送也會使用 hello 通道 tootake hello **GetImage**傳回值，並將它轉譯成 HTTP GETRESPONSE hello 用戶端瀏覽器。
12. 從 hello**建置**功能表上，按一下 **建置方案**tooconfirm hello 精確度的工作為止。

### <a name="example"></a>範例
下列程式碼的 hello 顯示定義的 WCF 轉送合約的基本介面。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>步驟 3： 實作 REST 式 WCF 服務合約 toouse 服務匯流排
建立 rest 式 WCF 轉送服務，您必須先建立使用介面定義的 hello 合約。 hello 下一個步驟是 tooimplement hello 介面。 這項作業包括建立類別，名為**ImageService**實作使用者定義的 hello **IImageContract**介面。 實作 hello 合約之後，接著您設定 hello 介面使用 App.config 檔案。 hello 設定檔包含 hello 應用程式，例如 hello hello 服務名稱、 hello 名稱 hello 合約和通訊協定都使用的 toocommunicate 與 hello 轉送服務的 hello 類型的必要資訊。 hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。

因為與 hello 先前步驟中，沒有實作 rest 式合約與 WCF 轉送合約的差異很小。

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>tooimplement rest 式服務匯流排合約
1. 建立新的類別，名為**ImageService**的 hello 的 hello 定義之後，直接**IImageContract**介面。 hello **ImageService**類別會實作 hello **IImageContract**介面。
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    類似 tooother 介面實作，您可以實作 hello 定義不同的檔案中。 不過，本教學課程，hello 實作會出現在相同檔案儲存為 hello 介面定義的 hello 和`Main()`方法。
2. 套用 hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx)屬性 toohello **IImageService** hello 類別的類別 tooindicate 是 WCF 合約的實作。
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    如先前所述，此命名空間不是傳統的命名空間。 相反地，它是 hello 識別 hello 合約的 WCF 架構的一部分。 如需詳細資訊，請參閱 hello[資料合約名稱](https://msdn.microsoft.com/library/ms731045.aspx)hello WCF 文件中的主題。
3. 將.jpg 影像 tooyour 專案中。  
   
    這是一個 hello 服務 hello 接收瀏覽器中顯示的圖片。 以滑鼠右鍵按一下您的專案，然後按一下 [加入]。 然後按一下 [現有項目]。 使用 hello**加入現有項目**對話方塊方塊 toobrowse tooan 和適當的.jpg，然後按一下**新增**。
   
    加入時 hello 檔案，請確定**所有檔案**toohello 下一步的 hello 下拉式清單中選取**檔案名稱：**欄位。 本教學課程的 hello rest 會假設該 hello hello 映像的名稱為"image.jpg"。 如果您有不同的檔案，您將會有 toorename hello 映像，或變更程式碼 toocompensate。
4. 確定執行服務的 hello 可以尋找 hello 映像檔，在 toomake**方案總管] 中**hello 映像檔，以滑鼠右鍵按一下，然後按一下 [**屬性**。 在 [hello**屬性**] 窗格中，設定**複製 tooOutput 目錄**太**更新時才複製**。
5. 新增參考 toohello **System.Drawing.dll** toohello 組件專案，以及將相關聯的 hello 下列`using`陳述式。  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. 在 hello **ImageService**類別中，加入 hello 下列建構函式載入 hello 點陣圖，並準備 toosend 它 toohello 用戶端瀏覽器。
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. 直接在 hello 先前的程式碼之後, 將 hello 面一行加入**GetImage**方法在 hello **ImageService**類別 tooreturn HTTP 訊息包含 hello 映像。
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    此實作會使用**MemoryStream** tooretrieve hello 映像，並準備進行串流處理 toohello 瀏覽器。 它會啟動 hello 資料流位置在零處，宣告為 jpeg，hello 串流處理內容及資料流的 hello 資訊。
8. 從 hello**建置**功能表上，按一下 **建置方案**。

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>toodefine hello 設定服務匯流排上執行 hello web 服務
1. 在**方案總管 中**，連按兩下**App.config** tooopen hello Visual Studio 編輯器中。
   
    hello **App.config**檔案包含 hello 服務名稱、 端點 （也就是 hello 位置 Azure 轉送會公開為用戶端和主機彼此 toocommunicate），以及繫結 （通訊協定都使用的 toocommunicate hello 類型）。 hello 主要的差異在於該 hello 設定服務端點會參考 tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding)繫結。
2. hello `<system.serviceModel>` XML 項目會定義一個或多個服務的 WCF 項目。 這裡是使用的 toodefine hello 服務名稱和端點。 在 hello 底部 hello`<system.serviceModel>`項目 (但仍在`<system.serviceModel>`)，新增`<bindings>`hello 內容之後的項目。 這會定義 hello hello 應用程式中使用的繫結。 您可以定義多個繫結，但在本教學課程中您只會定義一個。
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    hello 先前的程式碼定義的 WCF 轉送[WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding)繫結**relayClientAuthenticationType**設定得**無**。 這個設定表示使用此繫結的端點不需要用戶端認證。
3. 之後 hello`<bindings>`項目，加入`<services>`項目。 類似 toohello 繫結，您可以在單一設定檔中定義多個服務。 不過，您在本教學課程中只會定義一個。
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    此步驟會設定使用預先定義的 hello 預設的服務**webHttpRelayBinding**。 它也會使用預設 hello **sbTokenProvider**，定義在 hello 下一個步驟。
4. 之後 hello`<services>`項目，建立`<behaviors>`元素與 hello 內容之後，「 SAS_KEY"取代成 hello*共用存取簽章*(SAS) 金鑰，您先前取得的 hello [Azure 入口網站][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. 仍在 App.config 中，在 hello`<appSettings>`項目，使用您先前取得的 hello 入口網站的 hello 連接字串取代 hello 整個連接字串值。 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. 從 hello**建置**功能表上，按一下 **建置方案**toobuild hello 整個方案。

### <a name="example"></a>範例
hello 下列程式碼顯示 hello 合約和服務實作，以 REST 為基礎的服務上執行的服務匯流排使用 hello **WebHttpRelayBinding**繫結。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

hello 下列範例顯示 hello 與 hello 服務相關聯的 App.config 檔案。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>步驟 4： 主機 hello REST 式 WCF 服務 toouse Azure 轉送
此步驟說明如何 toorun web 服務的主控台應用程式使用 WCF 轉送。 Hello 範例 hello 程序中提供 hello 撰寫的程式碼在此步驟中的完整清單。

### <a name="toocreate-a-base-address-for-hello-service"></a>toocreate hello 服務的基底位址
1. 在 hello`Main()`函式宣告中，建立變數 toostore hello 命名空間，您的專案。 請確定 tooreplace `yourNamespace` hello hello 您先前建立的轉送命名空間名稱。
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    服務匯流排會使用您的唯一 URI 的命名空間 toocreate hello 名稱。
2. 建立`Uri`hello 基底地址的 hello 命名空間為基礎的 hello 服務的執行個體。
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate 及設定 hello web 服務主機
* 建立 hello web 服務主機，請使用本節稍早建立的 hello URI 位址。
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    hello 具現化 hello 主應用程式的 WCF 物件 hello 服務主機。 此範例會將它 hello 類型要 toocreate 的主機 ( **ImageService**)，並也 hello 想 tooexpose hello 主應用程式的位址。

### <a name="toorun-hello-web-service-host"></a>toorun hello web 服務主機
1. 開啟 hello 服務。
   
    ```csharp
    host.Open();
    ```
    hello 服務現在正在執行。
2. 顯示訊息指示 hello 服務正在執行，且 toostop hello 服務的方式。
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. 完成後，關閉 hello 服務主機。
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>範例
hello 下列範例包含主控台應用程式中的 hello 教學課程和主機 hello 服務中的 hello 服務合約和實作，從上一個步驟。 編譯 hello 遵循成名為 ImageListener.exe 的可執行檔的程式碼。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>編譯 hello 程式碼
在建置之後 hello 方案，下列 toorun hello 應用程式 hello:

1. 按**F5**，或瀏覽 toohello 可執行檔的位置 (ImageListener\bin\Debug\ImageListener.exe)，toorun hello 服務。 保持 hello 應用程式執行，它需要 tooperform hello 下一個步驟。
2. 複製並貼到瀏覽器 toosee hello 映像的 hello 命令提示字元中的 hello 位址。
3. 當您完成時，請按**Enter** hello 命令提示字元 視窗 tooclose hello 應用程式中。

## <a name="next-steps"></a>後續步驟
既然您已經建置使用 hello Service Bus 轉送服務的應用程式，請參閱下列文章 toolearn 更多關於 Azure 轉送 hello:

* [Azure 服務匯流排架構概觀](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Azure 轉送概觀](relay-what-is-it.md)
* [如何 toouse hello WCF 轉送服務的.NET](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
