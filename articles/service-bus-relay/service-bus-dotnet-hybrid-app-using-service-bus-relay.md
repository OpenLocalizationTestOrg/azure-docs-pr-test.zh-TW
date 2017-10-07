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
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="4e90a-103">使用 Azure WCF 轉送的 .NET 內部部署/雲端混合式應用程式</span><span class="sxs-lookup"><span data-stu-id="4e90a-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="4e90a-104">簡介</span><span class="sxs-lookup"><span data-stu-id="4e90a-104">Introduction</span></span>

<span data-ttu-id="4e90a-105">本文將說明如何 toobuild 混合式雲端使用 Microsoft Azure 和 Visual Studio 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="4e90a-106">hello 教學課程假設您有使用 Azure 沒有先前的經驗。</span><span class="sxs-lookup"><span data-stu-id="4e90a-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="4e90a-107">在 30 分鐘內，您必須使用多個 Azure 資源上的應用程式和 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="4e90a-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="4e90a-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="4e90a-108">You will learn:</span></span>

* <span data-ttu-id="4e90a-109">如何 toocreate 或調整現有的 web 服務取用 web 解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e90a-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="4e90a-110">如何 toouse hello Azure 的 WCF 轉送服務 tooshare 資料之間的 Azure 應用程式和 web 服務裝載其他位置。</span><span class="sxs-lookup"><span data-stu-id="4e90a-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="4e90a-111">Azure 轉送如何透過混合式解決方案提供協助</span><span class="sxs-lookup"><span data-stu-id="4e90a-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="4e90a-112">商務解決方案通常被組成的自訂程式碼撰寫新 tootackle 唯一的商務需求和現有方案和已備妥的系統提供的功能組合。</span><span class="sxs-lookup"><span data-stu-id="4e90a-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="4e90a-113">解決方案架構設計人員開始 toouse hello 雲端的小數位數的需求和較低的營運成本更容易處理。</span><span class="sxs-lookup"><span data-stu-id="4e90a-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="4e90a-114">在此情況下，而是尋找他們想 tooleverage 為其方案的建置組塊為 hello 公司防火牆內，和從簡單的現有服務資產到達存取 hello 雲端解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e90a-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="4e90a-115">許多內部服務未建立或裝載就可以輕鬆地公開在 hello 公司網路邊緣的方式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="4e90a-116">[Azure 轉送](https://azure.microsoft.com/services/service-bus/)適合 hello 採取之現有的 Windows Communication Foundation (WCF) web 服務的使用案例，並讓這些服務，而不需要位於 hello 公司外安全地存取 toosolutions具侵入性變更 toohello 公司網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="4e90a-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="4e90a-117">這類的轉送服務仍會裝載於其現有的環境，但它們委派接聽內送工作階段與要求 toohello 雲端裝載的轉送服務。</span><span class="sxs-lookup"><span data-stu-id="4e90a-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="4e90a-118">Azure 轉送也可使用[共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md) 驗證，保護那些服務免受未經授權的存取。</span><span class="sxs-lookup"><span data-stu-id="4e90a-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="4e90a-119">解決方案案例</span><span class="sxs-lookup"><span data-stu-id="4e90a-119">Solution scenario</span></span>
<span data-ttu-id="4e90a-120">在本教學課程中，您將建立 ASP.NET 網站，可讓您 toosee hello 產品詳細目錄 頁面上的產品清單。</span><span class="sxs-lookup"><span data-stu-id="4e90a-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="4e90a-121">hello 教學課程假設您有現有的內部部署系統中的產品資訊，以及該系統會使用 Azure 轉送 tooreach。</span><span class="sxs-lookup"><span data-stu-id="4e90a-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="4e90a-122">這項模擬是由簡單主控台應用程式中執行的 Web 服務來進行，並由記憶體內的產品集支援。</span><span class="sxs-lookup"><span data-stu-id="4e90a-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="4e90a-123">將您自己電腦上會無法 toorun 此主控台應用程式，並部署至 Azure 的 hello web 角色。</span><span class="sxs-lookup"><span data-stu-id="4e90a-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="4e90a-124">如此一來，您會看到如何 hello hello Azure 資料中心中執行的 web 角色會確實呼叫您的電腦，即使您的電腦將會幾乎都位於後面至少一個防火牆和網路位址轉譯 (NAT) 層級。</span><span class="sxs-lookup"><span data-stu-id="4e90a-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="4e90a-125">設定 hello 開發環境</span><span class="sxs-lookup"><span data-stu-id="4e90a-125">Set up hello development environment</span></span>

<span data-ttu-id="4e90a-126">您可以開始開發 Azure 應用程式之前，下載 hello 工具，並設定您的開發環境：</span><span class="sxs-lookup"><span data-stu-id="4e90a-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="4e90a-127">安裝 hello Azure SDK for.NET，從 hello SDK[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="4e90a-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4e90a-128">在 hello **.NET**資料行中，按一下 hello 版本[Visual Studio](http://www.visualstudio.com)您使用。</span><span class="sxs-lookup"><span data-stu-id="4e90a-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="4e90a-129">hello 步驟在此教學課程使用 Visual Studio 2015，但也可使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="4e90a-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="4e90a-130">當系統提示 toorun 或儲存 hello 安裝程式時，按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="4e90a-131">在 hello **Web Platform Installer**，按一下 **安裝**並繼續進行 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="4e90a-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="4e90a-132">Hello 安裝完成之後，您將會擁有一切所需的 toostart toodevelop hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="4e90a-133">hello SDK 包含工具，讓您輕鬆地開發 Visual Studio 中的 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="4e90a-134">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="4e90a-134">Create a namespace</span></span>

<span data-ttu-id="4e90a-135">使用 toobegin hello 轉送功能，在 Azure 中的，您必須先建立服務命名空間。</span><span class="sxs-lookup"><span data-stu-id="4e90a-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="4e90a-136">命名空間提供範圍容器，可在應用程式內進行 Azure 資源定址。</span><span class="sxs-lookup"><span data-stu-id="4e90a-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="4e90a-137">請遵循 hello[這裡的指示](relay-create-namespace-portal.md)toocreate 轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="4e90a-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="4e90a-138">建立內部部署伺服器</span><span class="sxs-lookup"><span data-stu-id="4e90a-138">Create an on-premises server</span></span>

<span data-ttu-id="4e90a-139">首先，您將建置 (模擬) 內部部署產品目錄系統。</span><span class="sxs-lookup"><span data-stu-id="4e90a-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="4e90a-140">將會相當簡單。您可以查看這表示我們想 toointegrate 完整服務介面與實際的內部部署產品目錄系統。</span><span class="sxs-lookup"><span data-stu-id="4e90a-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="4e90a-141">這個專案是 Visual Studio 主控台應用程式，並使用 hello [Azure 服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)tooinclude hello 服務匯流排程式庫和組態設定。</span><span class="sxs-lookup"><span data-stu-id="4e90a-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="4e90a-142">建立 hello 專案</span><span class="sxs-lookup"><span data-stu-id="4e90a-142">Create hello project</span></span>

1. <span data-ttu-id="4e90a-143">使用系統管理員權限，啟動 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4e90a-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="4e90a-144">toodo，hello Visual Studio 程式圖示，以滑鼠右鍵按一下，然後按一下**系統管理員身分執行**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="4e90a-145">在 Visual Studio 中的 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="4e90a-146">從 [已安裝的範本] 的 [Visual C#] 下，按一下 [主控台應用程式 (.NET Framework]。</span><span class="sxs-lookup"><span data-stu-id="4e90a-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="4e90a-147">在 [hello**名稱**] 方塊中，輸入 hello 名稱**ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="4e90a-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="4e90a-148">按一下**確定**toocreate hello **ProductsServer**專案。</span><span class="sxs-lookup"><span data-stu-id="4e90a-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="4e90a-149">如果您已安裝 Visual Studio 的 hello NuGet 封裝管理員，請略過 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="4e90a-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="4e90a-150">否則，請造訪 [NuGet][NuGet]，然後按一下[安裝 NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)。</span><span class="sxs-lookup"><span data-stu-id="4e90a-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="4e90a-151">請遵循 hello 提示 tooinstall hello NuGet 封裝管理員，然後重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4e90a-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="4e90a-152">在 方案總管 中，以滑鼠右鍵按一下 hello **ProductsServer**專案，然後按一下 **管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="4e90a-153">按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="4e90a-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="4e90a-154">選取 hello **WindowsAzure.ServiceBus**封裝。</span><span class="sxs-lookup"><span data-stu-id="4e90a-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="4e90a-155">按一下**安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="4e90a-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="4e90a-156">請注意該 hello 需要用戶端組件現在會參考。</span><span class="sxs-lookup"><span data-stu-id="4e90a-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="4e90a-157">新增產品連絡人的新類別。</span><span class="sxs-lookup"><span data-stu-id="4e90a-157">Add a new class for your product contract.</span></span> <span data-ttu-id="4e90a-158">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ProductsServer**專案，然後按一下**新增**，然後按一下**類別**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="4e90a-159">在 [hello**名稱**] 方塊中，輸入 hello 名稱**ProductsContract.cs**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="4e90a-160">然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="4e90a-160">Then click **Add**.</span></span>
10. <span data-ttu-id="4e90a-161">在**ProductsContract.cs**，取代下列程式碼，其定義 hello 服務合約的 hello hello hello 命名空間定義。</span><span class="sxs-lookup"><span data-stu-id="4e90a-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

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
11. <span data-ttu-id="4e90a-162">在 Program.cs 中，請使用下列程式碼中，這會將 hello 設定檔服務和它的 hello 主機 hello 取代 hello 命名空間定義。</span><span class="sxs-lookup"><span data-stu-id="4e90a-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

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
12. <span data-ttu-id="4e90a-163">在 方案總管 中，按兩下 hello **App.config**檔案 tooopen hello Visual Studio 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="4e90a-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="4e90a-164">在 hello 底部 hello`<system.ServiceModel>`項目 (但仍在`<system.ServiceModel>`)，加入下列 XML 程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e90a-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="4e90a-165">要確定 tooreplace *yourServiceNamespace* hello 名稱，為您的命名空間和*yourKey*與 hello hello 入口網站從先前擷取的 SAS 金鑰：</span><span class="sxs-lookup"><span data-stu-id="4e90a-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

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
13. <span data-ttu-id="4e90a-166">仍在 App.config 中，在 hello`<appSettings>`項目，取代 hello 連接與您先前取得的 hello 入口網站的 hello 連接字串的字串值。</span><span class="sxs-lookup"><span data-stu-id="4e90a-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="4e90a-167">按**Ctrl + Shift + B**或從 hello**建置**功能表上，按一下 **建置方案**toobuild hello 應用程式，並確認工作的 hello 準確性為止。</span><span class="sxs-lookup"><span data-stu-id="4e90a-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="4e90a-168">建立 ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e90a-168">Create an ASP.NET application</span></span>

<span data-ttu-id="4e90a-169">在本節中，您將建置簡單的 ASP.NET 應用程式，來顯示從產品服務擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="4e90a-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="4e90a-170">建立 hello 專案</span><span class="sxs-lookup"><span data-stu-id="4e90a-170">Create hello project</span></span>

1. <span data-ttu-id="4e90a-171">確定 Visual Studio 是以系統管理員權限來執行。</span><span class="sxs-lookup"><span data-stu-id="4e90a-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="4e90a-172">在 Visual Studio 中的 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="4e90a-173">從 [已安裝的範本] 的 [Visual C#] 下，按一下 [ASP.NET Web 應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="4e90a-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="4e90a-174">名稱 hello 專案**ProductsPortal**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="4e90a-175">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4e90a-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="4e90a-176">從 hello **ASP.NET 範本**列入 hello**新的 ASP.NET Web 應用程式**] 對話方塊中，按一下 [ **MVC**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="4e90a-177">按一下 hello**變更驗證** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4e90a-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="4e90a-178">在 hello**變更驗證**對話方塊方塊中，確定**非驗證**已選取，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="4e90a-179">在本教學課程中，您會部署不需要使用者登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="4e90a-180">在 hello**新的 ASP.NET Web 應用程式** 對話方塊中，按一下 **確定**toocreate hello MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="4e90a-181">您現在必須設定新 Web 應用程式的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="4e90a-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="4e90a-182">Hello 中的 hello 步驟[發行本文 tooAzure 節](../app-service-web/app-service-web-get-started-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="4e90a-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="4e90a-183">然後，傳回 toothis 教學課程，並繼續進行 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="4e90a-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="4e90a-184">在 [方案總管] 中，於 [模型] 上按一下滑鼠右鍵、按一下 [新增]，再按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="4e90a-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="4e90a-185">在 [hello**名稱**] 方塊中，輸入 hello 名稱**Product.cs**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="4e90a-186">然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="4e90a-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="4e90a-187">修改 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e90a-187">Modify hello web application</span></span>

1. <span data-ttu-id="4e90a-188">在 Visual Studio 中的 hello Product.cs 檔案，取代 hello 下列程式碼中的 hello 現有命名空間定義。</span><span class="sxs-lookup"><span data-stu-id="4e90a-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

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
2. <span data-ttu-id="4e90a-189">在 方案總管 中，展開 hello**控制器**資料夾，然後按兩下 hello **HomeController.cs**檔案 tooopen 在 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4e90a-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="4e90a-190">在**HomeController.cs**，取代下列程式碼的 hello hello 現有命名空間定義。</span><span class="sxs-lookup"><span data-stu-id="4e90a-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

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
4. <span data-ttu-id="4e90a-191">在方案總管 中，依序展開 hello Views\Shared 資料夾中按兩下**_Layout.cshtml** tooopen hello Visual Studio 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="4e90a-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="4e90a-192">將所有**我的 ASP.NET 應用程式**太**LITWARE 的產品**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="4e90a-193">移除 hello**首頁**，**有關**，和**連絡人**連結。</span><span class="sxs-lookup"><span data-stu-id="4e90a-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="4e90a-194">在下列範例的 hello，刪除 hello 反白顯示程式碼。</span><span class="sxs-lookup"><span data-stu-id="4e90a-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="4e90a-195">在方案總管 中，依序展開 hello Views\Home 資料夾中按兩下**Index.cshtml** tooopen hello Visual Studio 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="4e90a-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="4e90a-196">取代下列程式碼的 hello hello 整個 hello 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="4e90a-196">Replace hello entire contents of hello file with hello following code.</span></span>

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
8. <span data-ttu-id="4e90a-197">工作的 tooverify hello 準確性為止，您可以按**Ctrl + Shift + B** toobuild hello 專案。</span><span class="sxs-lookup"><span data-stu-id="4e90a-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="4e90a-198">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e90a-198">Run hello app locally</span></span>

<span data-ttu-id="4e90a-199">執行 hello 應用程式 tooverify 正常運作。</span><span class="sxs-lookup"><span data-stu-id="4e90a-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="4e90a-200">請確認**ProductsPortal**是 hello 現用專案。</span><span class="sxs-lookup"><span data-stu-id="4e90a-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="4e90a-201">以滑鼠右鍵按一下方案總管 中的 hello 專案名稱，然後選取**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="4e90a-202">在 Visual Studio 中按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="4e90a-203">您的應用程式應該就會出現在瀏覽器中並正在執行。</span><span class="sxs-lookup"><span data-stu-id="4e90a-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="4e90a-204">Hello 片段放在一起</span><span class="sxs-lookup"><span data-stu-id="4e90a-204">Put hello pieces together</span></span>

<span data-ttu-id="4e90a-205">hello 下一個步驟是 toohook hello 在內部部署產品的伺服器以 hello ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="4e90a-206">如果它尚未開啟，Visual Studio 中重新開啟 hello **ProductsPortal** hello 中建立的專案[建立 ASP.NET 應用程式](#create-an-aspnet-application)> 一節。</span><span class="sxs-lookup"><span data-stu-id="4e90a-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="4e90a-207">類似 toohello 步驟在 hello 「 建立為內部伺服器 」 區段中，加入 hello NuGet 封裝 toohello 專案參考。</span><span class="sxs-lookup"><span data-stu-id="4e90a-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="4e90a-208">在 方案總管 中，以滑鼠右鍵按一下 hello **ProductsPortal**專案，然後按一下 **管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="4e90a-209">搜尋 「 Service Bus 」 和選取 hello **WindowsAzure.ServiceBus**項目。</span><span class="sxs-lookup"><span data-stu-id="4e90a-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="4e90a-210">然後完成 hello 安裝並關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4e90a-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="4e90a-211">在 方案總管 中，以滑鼠右鍵按一下 hello **ProductsPortal**專案，然後按一下 **新增**，然後**現有項目**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="4e90a-212">瀏覽 toohello **ProductsContract.cs**檔案從 hello **ProductsServer**主控台專案。</span><span class="sxs-lookup"><span data-stu-id="4e90a-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="4e90a-213">按一下 toohighlight ProductsContract.cs。</span><span class="sxs-lookup"><span data-stu-id="4e90a-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="4e90a-214">按一下向下箭號 hello 下一步太**新增**，然後按一下 **加入做為連結**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="4e90a-215">現在開啟 hello **HomeController.cs**檔案 hello Visual Studio 編輯器中，然後以下列程式碼的 hello 取代 hello 命名空間定義。</span><span class="sxs-lookup"><span data-stu-id="4e90a-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="4e90a-216">要確定 tooreplace *yourServiceNamespace* hello 名稱，為您的服務命名空間和*yourKey*附有 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="4e90a-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="4e90a-217">這會讓 hello client toocall hello 在內部部署服務，傳回 hello 呼叫 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="4e90a-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

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
7. <span data-ttu-id="4e90a-218">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ProductsPortal**方案 （請確定 tooright 按一下 hello 解決方案，不 hello 專案）。</span><span class="sxs-lookup"><span data-stu-id="4e90a-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="4e90a-219">按一下 [新增]，然後按一下 [現有專案]。</span><span class="sxs-lookup"><span data-stu-id="4e90a-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="4e90a-220">瀏覽 toohello **ProductsServer**專案，然後按兩下 hello **ProductsServer.csproj**方案檔案 tooadd 它。</span><span class="sxs-lookup"><span data-stu-id="4e90a-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="4e90a-221">**ProductsServer**必須以執行順序 toodisplay hello 資料**ProductsPortal**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="4e90a-222">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ProductsPortal**方案，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="4e90a-223">hello**屬性頁**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="4e90a-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="4e90a-224">在 hello 左側，按一下**啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="4e90a-225">在 hello 右邊，按一下 **多個啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="4e90a-226">請確認**ProductsServer**和**ProductsPortal**出現，請使用**啟動**設為兩個 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="4e90a-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="4e90a-227">仍在 hello**屬性**對話方塊中，按一下 **專案相依性**hello 左側上。</span><span class="sxs-lookup"><span data-stu-id="4e90a-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="4e90a-228">在 hello**專案**清單中，按一下**ProductsServer**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="4e90a-229">確定未選取 [ProductsPortal]。</span><span class="sxs-lookup"><span data-stu-id="4e90a-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="4e90a-230">在 hello**專案**清單中，按一下**ProductsPortal**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="4e90a-231">確定已選取 [ProductsServer]。</span><span class="sxs-lookup"><span data-stu-id="4e90a-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="4e90a-232">按一下**確定**在 hello**屬性頁** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4e90a-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="4e90a-233">在本機執行 hello 專案</span><span class="sxs-lookup"><span data-stu-id="4e90a-233">Run hello project locally</span></span>

<span data-ttu-id="4e90a-234">在本機，tootest hello 應用程式 Visual Studio 中的按**F5**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="4e90a-235">hello 在內部部署伺服器 (**ProductsServer**) 應該開始第一次，然後在 hello **ProductsPortal**應用程式應該啟動瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="4e90a-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="4e90a-236">此時，您會看到該 hello 產品存貨列出從 hello 產品服務在內部部署系統擷取資料。</span><span class="sxs-lookup"><span data-stu-id="4e90a-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="4e90a-237">按**重新整理**上 hello **ProductsPortal**頁面。</span><span class="sxs-lookup"><span data-stu-id="4e90a-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="4e90a-238">每次您重新整理 hello 頁面時，您會看到顯示訊息的 hello 伺服器應用程式時`GetProducts()`從**ProductsServer**呼叫。</span><span class="sxs-lookup"><span data-stu-id="4e90a-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="4e90a-239">關閉這兩個應用程式，然後再繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="4e90a-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="4e90a-240">部署 hello ProductsPortal 專案 tooan Azure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e90a-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="4e90a-241">hello 下一個步驟是 toorepublish hello Azure Web 應用程式**ProductsPortal**前端。</span><span class="sxs-lookup"><span data-stu-id="4e90a-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="4e90a-242">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="4e90a-242">Do hello following:</span></span>

1. <span data-ttu-id="4e90a-243">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ProductsPortal**專案，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="4e90a-244">然後，按一下 **發行**上 hello**發行**頁面。</span><span class="sxs-lookup"><span data-stu-id="4e90a-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4e90a-245">您可能會看到錯誤訊息中的 hello 瀏覽器視窗時 hello **ProductsPortal** hello 部署之後自動啟動 web 專案。</span><span class="sxs-lookup"><span data-stu-id="4e90a-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="4e90a-246">這預期，就會發生 hello **ProductsServer**應用程式不尚未執行。</span><span class="sxs-lookup"><span data-stu-id="4e90a-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="4e90a-247">複製 hello URL 的 hello 部署 web 應用程式，將會需要 hello 下一個步驟中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="4e90a-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="4e90a-248">您也可以從 Visual Studio 中的 hello Azure 應用程式服務活動視窗取得此 URL:</span><span class="sxs-lookup"><span data-stu-id="4e90a-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="4e90a-249">關閉 hello 瀏覽器視窗 toostop hello 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="4e90a-250">將 ProductsPortal 設定為 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e90a-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="4e90a-251">之前執行 hello hello 雲端中應用程式，您必須確定**ProductsPortal**從 web 應用程式的 Visual Studio 中啟動。</span><span class="sxs-lookup"><span data-stu-id="4e90a-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="4e90a-252">在 Visual Studio 中，以滑鼠右鍵按一下 hello **ProductsPortal**專案，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="4e90a-253">在 hello 左側資料行中，按一下  **Web**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="4e90a-254">在 [hello**起始動作**區段中，按一下 hello**起始 URL**按鈕，並在 hello] 文字方塊中輸入您先前已部署的 web 應用程式; hello URL，例如`http://productsportal1234567890.azurewebsites.net/`。</span><span class="sxs-lookup"><span data-stu-id="4e90a-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="4e90a-255">從 hello**檔案**功能表在 Visual Studio 中，按一下**全部儲存**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="4e90a-256">從 Visual Studio 中的 hello 建置] 功能表，按一下 [**重建方案**。</span><span class="sxs-lookup"><span data-stu-id="4e90a-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="4e90a-257">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e90a-257">Run hello application</span></span>

1. <span data-ttu-id="4e90a-258">按 F5 toobuild，並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="4e90a-259">hello 在內部部署伺服器 (hello **ProductsServer**主控台應用程式) 應該開始第一次，然後在 hello **ProductsPortal** hello 遵循畫面所示，在瀏覽器視窗中，應該啟動應用程式擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="4e90a-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="4e90a-260">再次請注意該 hello 產品存貨列出從 hello 產品服務在內部部署系統擷取資料並顯示 hello web 應用程式中的該資料。</span><span class="sxs-lookup"><span data-stu-id="4e90a-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="4e90a-261">檢查確定 hello URL toomake， **ProductsPortal** hello 雲端，為 Azure web 應用程式中執行。</span><span class="sxs-lookup"><span data-stu-id="4e90a-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="4e90a-262">hello **ProductsServer**主控台應用程式必須執行，而且要能 tooserve hello 資料 toohello **ProductsPortal**應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e90a-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="4e90a-263">如果 hello 瀏覽器會顯示錯誤，請等候幾秒，讓**ProductsServer** tooload 和下列顯示 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="4e90a-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="4e90a-264">然後按下**重新整理**hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="4e90a-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="4e90a-265">在 hello 瀏覽器按**重新整理**上 hello **ProductsPortal**頁面。</span><span class="sxs-lookup"><span data-stu-id="4e90a-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="4e90a-266">每次您重新整理 hello 頁面時，您會看到顯示訊息的 hello 伺服器應用程式時`GetProducts()`從**ProductsServer**呼叫。</span><span class="sxs-lookup"><span data-stu-id="4e90a-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="4e90a-267">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e90a-267">Next steps</span></span>

<span data-ttu-id="4e90a-268">toolearn 深入了解 Azure 轉送，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="4e90a-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="4e90a-269">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="4e90a-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="4e90a-270">如何 toouse 轉送</span><span class="sxs-lookup"><span data-stu-id="4e90a-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
