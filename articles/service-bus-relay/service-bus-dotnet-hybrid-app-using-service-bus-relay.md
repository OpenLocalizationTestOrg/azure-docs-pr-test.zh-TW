---
title: "aaaAzure WCF 轉送混合式雲端上的內部部署/應用程式 (.NET) |Microsoft 文件"
description: "深入了解如何使用 Azure 的 WCF 轉送 toocreate.NET 雲端上的內部部署/混合式應用程式。"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>使用 Azure WCF 轉送的 .NET 內部部署/雲端混合式應用程式
## <a name="introduction"></a>簡介

本文將說明如何 toobuild 混合式雲端使用 Microsoft Azure 和 Visual Studio 的應用程式。 hello 教學課程假設您有使用 Azure 沒有先前的經驗。 在 30 分鐘內，您必須使用多個 Azure 資源上的應用程式和 hello 雲端中執行。

您將了解：

* 如何 toocreate 或調整現有的 web 服務取用 web 解決方案。
* 如何 toouse hello Azure 的 WCF 轉送服務 tooshare 資料之間的 Azure 應用程式和 web 服務裝載其他位置。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Azure 轉送如何透過混合式解決方案提供協助

商務解決方案通常被組成的自訂程式碼撰寫新 tootackle 唯一的商務需求和現有方案和已備妥的系統提供的功能組合。

解決方案架構設計人員開始 toouse hello 雲端的小數位數的需求和較低的營運成本更容易處理。 在此情況下，而是尋找他們想 tooleverage 為其方案的建置組塊為 hello 公司防火牆內，和從簡單的現有服務資產到達存取 hello 雲端解決方案。 許多內部服務未建立或裝載就可以輕鬆地公開在 hello 公司網路邊緣的方式。

[Azure 轉送](https://azure.microsoft.com/services/service-bus/)適合 hello 採取之現有的 Windows Communication Foundation (WCF) web 服務的使用案例，並讓這些服務，而不需要位於 hello 公司外安全地存取 toosolutions具侵入性變更 toohello 公司網路基礎結構。 這類的轉送服務仍會裝載於其現有的環境，但它們委派接聽內送工作階段與要求 toohello 雲端裝載的轉送服務。 Azure 轉送也可使用[共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md) 驗證，保護那些服務免受未經授權的存取。

## <a name="solution-scenario"></a>解決方案案例
在本教學課程中，您將建立 ASP.NET 網站，可讓您 toosee hello 產品詳細目錄 頁面上的產品清單。

![][0]

hello 教學課程假設您有現有的內部部署系統中的產品資訊，以及該系統會使用 Azure 轉送 tooreach。 這項模擬是由簡單主控台應用程式中執行的 Web 服務來進行，並由記憶體內的產品集支援。 將您自己電腦上會無法 toorun 此主控台應用程式，並部署至 Azure 的 hello web 角色。 如此一來，您會看到如何 hello hello Azure 資料中心中執行的 web 角色會確實呼叫您的電腦，即使您的電腦將會幾乎都位於後面至少一個防火牆和網路位址轉譯 (NAT) 層級。

## <a name="set-up-hello-development-environment"></a>設定 hello 開發環境

您可以開始開發 Azure 應用程式之前，下載 hello 工具，並設定您的開發環境：

1. 安裝 hello Azure SDK for.NET，從 hello SDK[下載頁面](https://azure.microsoft.com/downloads/)。
2. 在 hello **.NET**資料行中，按一下 hello 版本[Visual Studio](http://www.visualstudio.com)您使用。 hello 步驟在此教學課程使用 Visual Studio 2015，但也可使用 Visual Studio 2017。
3. 當系統提示 toorun 或儲存 hello 安裝程式時，按一下**執行**。
4. 在 hello **Web Platform Installer**，按一下 **安裝**並繼續進行 hello 安裝。
5. Hello 安裝完成之後，您將會擁有一切所需的 toostart toodevelop hello 應用程式。 hello SDK 包含工具，讓您輕鬆地開發 Visual Studio 中的 Azure 應用程式。

## <a name="create-a-namespace"></a>建立命名空間

使用 toobegin hello 轉送功能，在 Azure 中的，您必須先建立服務命名空間。 命名空間提供範圍容器，可在應用程式內進行 Azure 資源定址。 請遵循 hello[這裡的指示](relay-create-namespace-portal.md)toocreate 轉送命名空間。

## <a name="create-an-on-premises-server"></a>建立內部部署伺服器

首先，您將建置 (模擬) 內部部署產品目錄系統。 將會相當簡單。您可以查看這表示我們想 toointegrate 完整服務介面與實際的內部部署產品目錄系統。

這個專案是 Visual Studio 主控台應用程式，並使用 hello [Azure 服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)tooinclude hello 服務匯流排程式庫和組態設定。

### <a name="create-hello-project"></a>建立 hello 專案

1. 使用系統管理員權限，啟動 Microsoft Visual Studio。 toodo，hello Visual Studio 程式圖示，以滑鼠右鍵按一下，然後按一下**系統管理員身分執行**。
2. 在 Visual Studio 中的 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。
3. 從 [已安裝的範本] 的 [Visual C#] 下，按一下 [主控台應用程式 (.NET Framework]。 在 [hello**名稱**] 方塊中，輸入 hello 名稱**ProductsServer**:

   ![][11]
4. 按一下**確定**toocreate hello **ProductsServer**專案。
5. 如果您已安裝 Visual Studio 的 hello NuGet 封裝管理員，請略過 toohello 下一個步驟。 否則，請造訪 [NuGet][NuGet]，然後按一下[安裝 NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)。 請遵循 hello 提示 tooinstall hello NuGet 封裝管理員，然後重新啟動 Visual Studio。
6. 在 方案總管 中，以滑鼠右鍵按一下 hello **ProductsServer**專案，然後按一下 **管理 NuGet 封裝**。
7. 按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。 選取 hello **WindowsAzure.ServiceBus**封裝。
8. 按一下**安裝**，並接受使用規定 hello。

   ![][13]

   請注意該 hello 需要用戶端組件現在會參考。
8. 新增產品連絡人的新類別。 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ProductsServer**專案，然後按一下**新增**，然後按一下**類別**。
9. 在 [hello**名稱**] 方塊中，輸入 hello 名稱**ProductsContract.cs**。 然後按一下 [ **新增**]。
10. 在**ProductsContract.cs**，取代下列程式碼，其定義 hello 服務合約的 hello hello hello 命名空間定義。

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. 在 Program.cs 中，請使用下列程式碼中，這會將 hello 設定檔服務和它的 hello 主機 hello 取代 hello 命名空間定義。

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. 在 方案總管 中，按兩下 hello **App.config**檔案 tooopen hello Visual Studio 編輯器中。 在 hello 底部 hello`<system.ServiceModel>`項目 (但仍在`<system.ServiceModel>`)，加入下列 XML 程式碼的 hello。 要確定 tooreplace *yourServiceNamespace* hello 名稱，為您的命名空間和*yourKey*與 hello hello 入口網站從先前擷取的 SAS 金鑰：

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. 仍在 App.config 中，在 hello`<appSettings>`項目，取代 hello 連接與您先前取得的 hello 入口網站的 hello 連接字串的字串值。

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. 按**Ctrl + Shift + B**或從 hello**建置**功能表上，按一下 **建置方案**toobuild hello 應用程式，並確認工作的 hello 準確性為止。

## <a name="create-an-aspnet-application"></a>建立 ASP.NET 應用程式

在本節中，您將建置簡單的 ASP.NET 應用程式，來顯示從產品服務擷取的資料。

### <a name="create-hello-project"></a>建立 hello 專案

1. 確定 Visual Studio 是以系統管理員權限來執行。
2. 在 Visual Studio 中的 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。
3. 從 [已安裝的範本] 的 [Visual C#] 下，按一下 [ASP.NET Web 應用程式 (.NET Framework)]。 名稱 hello 專案**ProductsPortal**。 然後按一下 [確定] 。

   ![][15]

4. 從 hello **ASP.NET 範本**列入 hello**新的 ASP.NET Web 應用程式**] 對話方塊中，按一下 [ **MVC**。

   ![][16]

6. 按一下 hello**變更驗證** 按鈕。 在 hello**變更驗證**對話方塊方塊中，確定**非驗證**已選取，然後按一下**確定**。 在本教學課程中，您會部署不需要使用者登入的應用程式。

    ![][18]

7. 在 hello**新的 ASP.NET Web 應用程式** 對話方塊中，按一下 **確定**toocreate hello MVC 應用程式。
8. 您現在必須設定新 Web 應用程式的 Azure 資源。 Hello 中的 hello 步驟[發行本文 tooAzure 節](../app-service-web/app-service-web-get-started-dotnet.md)。 然後，傳回 toothis 教學課程，並繼續進行 toohello 下一個步驟。
10. 在 [方案總管] 中，於 [模型] 上按一下滑鼠右鍵、按一下 [新增]，再按一下 [類別]。 在 [hello**名稱**] 方塊中，輸入 hello 名稱**Product.cs**。 然後按一下 [ **新增**]。

    ![][17]

### <a name="modify-hello-web-application"></a>修改 hello web 應用程式

1. 在 Visual Studio 中的 hello Product.cs 檔案，取代 hello 下列程式碼中的 hello 現有命名空間定義。

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. 在 方案總管 中，展開 hello**控制器**資料夾，然後按兩下 hello **HomeController.cs**檔案 tooopen 在 Visual Studio。
3. 在**HomeController.cs**，取代下列程式碼的 hello hello 現有命名空間定義。

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. 在方案總管 中，依序展開 hello Views\Shared 資料夾中按兩下**_Layout.cshtml** tooopen hello Visual Studio 編輯器中。
5. 將所有**我的 ASP.NET 應用程式**太**LITWARE 的產品**。
6. 移除 hello**首頁**，**有關**，和**連絡人**連結。 在下列範例的 hello，刪除 hello 反白顯示程式碼。

    ![][41]

7. 在方案總管 中，依序展開 hello Views\Home 資料夾中按兩下**Index.cshtml** tooopen hello Visual Studio 編輯器中。 取代下列程式碼的 hello hello 整個 hello 檔案的內容。

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. 工作的 tooverify hello 準確性為止，您可以按**Ctrl + Shift + B** toobuild hello 專案。

### <a name="run-hello-app-locally"></a>在本機執行 hello 應用程式

執行 hello 應用程式 tooverify 正常運作。

1. 請確認**ProductsPortal**是 hello 現用專案。 以滑鼠右鍵按一下方案總管 中的 hello 專案名稱，然後選取**設定為啟始專案**。
2. 在 Visual Studio 中按 **F5**。
3. 您的應用程式應該就會出現在瀏覽器中並正在執行。

   ![][21]

## <a name="put-hello-pieces-together"></a>Hello 片段放在一起

hello 下一個步驟是 toohook hello 在內部部署產品的伺服器以 hello ASP.NET 應用程式。

1. 如果它尚未開啟，Visual Studio 中重新開啟 hello **ProductsPortal** hello 中建立的專案[建立 ASP.NET 應用程式](#create-an-aspnet-application)> 一節。
2. 類似 toohello 步驟在 hello 「 建立為內部伺服器 」 區段中，加入 hello NuGet 封裝 toohello 專案參考。 在 方案總管 中，以滑鼠右鍵按一下 hello **ProductsPortal**專案，然後按一下 **管理 NuGet 封裝**。
3. 搜尋 「 Service Bus 」 和選取 hello **WindowsAzure.ServiceBus**項目。 然後完成 hello 安裝並關閉此對話方塊。
4. 在 方案總管 中，以滑鼠右鍵按一下 hello **ProductsPortal**專案，然後按一下 **新增**，然後**現有項目**。
5. 瀏覽 toohello **ProductsContract.cs**檔案從 hello **ProductsServer**主控台專案。 按一下 toohighlight ProductsContract.cs。 按一下向下箭號 hello 下一步太**新增**，然後按一下 **加入做為連結**。

   ![][24]

6. 現在開啟 hello **HomeController.cs**檔案 hello Visual Studio 編輯器中，然後以下列程式碼的 hello 取代 hello 命名空間定義。 要確定 tooreplace *yourServiceNamespace* hello 名稱，為您的服務命名空間和*yourKey*附有 SAS 金鑰。 這會讓 hello client toocall hello 在內部部署服務，傳回 hello 呼叫 hello 結果。

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ProductsPortal**方案 （請確定 tooright 按一下 hello 解決方案，不 hello 專案）。 按一下 [新增]，然後按一下 [現有專案]。
8. 瀏覽 toohello **ProductsServer**專案，然後按兩下 hello **ProductsServer.csproj**方案檔案 tooadd 它。
9. **ProductsServer**必須以執行順序 toodisplay hello 資料**ProductsPortal**。 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ProductsPortal**方案，然後按一下**屬性**。 hello**屬性頁**對話方塊隨即出現。
10. 在 hello 左側，按一下**啟始專案**。 在 hello 右邊，按一下 **多個啟始專案**。 請確認**ProductsServer**和**ProductsPortal**出現，請使用**啟動**設為兩個 hello 動作。

      ![][25]

11. 仍在 hello**屬性**對話方塊中，按一下 **專案相依性**hello 左側上。
12. 在 hello**專案**清單中，按一下**ProductsServer**。 確定未選取 [ProductsPortal]。
13. 在 hello**專案**清單中，按一下**ProductsPortal**。 確定已選取 [ProductsServer]。

    ![][26]

14. 按一下**確定**在 hello**屬性頁** 對話方塊。

## <a name="run-hello-project-locally"></a>在本機執行 hello 專案

在本機，tootest hello 應用程式 Visual Studio 中的按**F5**。 hello 在內部部署伺服器 (**ProductsServer**) 應該開始第一次，然後在 hello **ProductsPortal**應用程式應該啟動瀏覽器視窗中。 此時，您會看到該 hello 產品存貨列出從 hello 產品服務在內部部署系統擷取資料。

![][10]

按**重新整理**上 hello **ProductsPortal**頁面。 每次您重新整理 hello 頁面時，您會看到顯示訊息的 hello 伺服器應用程式時`GetProducts()`從**ProductsServer**呼叫。

關閉這兩個應用程式，然後再繼續 toohello 下一個步驟。

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>部署 hello ProductsPortal 專案 tooan Azure web 應用程式

hello 下一個步驟是 toorepublish hello Azure Web 應用程式**ProductsPortal**前端。 請勿 hello 遵循：

1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ProductsPortal**專案，然後按一下**發行**。 然後，按一下 **發行**上 hello**發行**頁面。

  > [!NOTE]
  > 您可能會看到錯誤訊息中的 hello 瀏覽器視窗時 hello **ProductsPortal** hello 部署之後自動啟動 web 專案。 這預期，就會發生 hello **ProductsServer**應用程式不尚未執行。
>
>

2. 複製 hello URL 的 hello 部署 web 應用程式，將會需要 hello 下一個步驟中的 hello URL。 您也可以從 Visual Studio 中的 hello Azure 應用程式服務活動視窗取得此 URL:

  ![][9]

3. 關閉 hello 瀏覽器視窗 toostop hello 執行應用程式。

### <a name="set-productsportal-as-web-app"></a>將 ProductsPortal 設定為 Web 應用程式

之前執行 hello hello 雲端中應用程式，您必須確定**ProductsPortal**從 web 應用程式的 Visual Studio 中啟動。

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello **ProductsPortal**專案，然後按一下**屬性**。
2. 在 hello 左側資料行中，按一下  **Web**。
3. 在 [hello**起始動作**區段中，按一下 hello**起始 URL**按鈕，並在 hello] 文字方塊中輸入您先前已部署的 web 應用程式; hello URL，例如`http://productsportal1234567890.azurewebsites.net/`。

    ![][27]

4. 從 hello**檔案**功能表在 Visual Studio 中，按一下**全部儲存**。
5. 從 Visual Studio 中的 hello 建置] 功能表，按一下 [**重建方案**。

## <a name="run-hello-application"></a>執行 hello 應用程式

1. 按 F5 toobuild，並執行 hello 應用程式。 hello 在內部部署伺服器 (hello **ProductsServer**主控台應用程式) 應該開始第一次，然後在 hello **ProductsPortal** hello 遵循畫面所示，在瀏覽器視窗中，應該啟動應用程式擷取畫面。 再次請注意該 hello 產品存貨列出從 hello 產品服務在內部部署系統擷取資料並顯示 hello web 應用程式中的該資料。 檢查確定 hello URL toomake， **ProductsPortal** hello 雲端，為 Azure web 應用程式中執行。

   ![][1]

   > [!IMPORTANT]
   > hello **ProductsServer**主控台應用程式必須執行，而且要能 tooserve hello 資料 toohello **ProductsPortal**應用程式。 如果 hello 瀏覽器會顯示錯誤，請等候幾秒，讓**ProductsServer** tooload 和下列顯示 hello 訊息。 然後按下**重新整理**hello 瀏覽器中。
   >
   >

   ![][37]
2. 在 hello 瀏覽器按**重新整理**上 hello **ProductsPortal**頁面。 每次您重新整理 hello 頁面時，您會看到顯示訊息的 hello 伺服器應用程式時`GetProducts()`從**ProductsServer**呼叫。

    ![][38]

## <a name="next-steps"></a>後續步驟

toolearn 深入了解 Azure 轉送，請參閱下列資源的 hello:  

* [什麼是 Azure 轉送？](relay-what-is-it.md)  
* [如何 toouse 轉送](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
