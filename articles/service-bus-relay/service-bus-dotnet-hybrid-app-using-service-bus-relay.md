---
title: "Azure WCF 轉送混合式內部部署/雲端應用程式 (.NET) | Microsoft Docs"
description: "了解如何建立使用 Azure WCF 轉送的 .NET 內部部署/雲端混合式應用程式。"
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
ms.openlocfilehash: 366922a083b9d18ef50e04eb8b459d2725315e1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="7452e-103">使用 Azure WCF 轉送的 .NET 內部部署/雲端混合式應用程式</span><span class="sxs-lookup"><span data-stu-id="7452e-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="7452e-104">簡介</span><span class="sxs-lookup"><span data-stu-id="7452e-104">Introduction</span></span>

<span data-ttu-id="7452e-105">本文示範如何使用 Microsoft Azure 和 Visual Studio 建置混合式雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="7452e-105">This article shows how to build a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="7452e-106">本教學課程假設您先前沒有使用 Azure 的經驗。</span><span class="sxs-lookup"><span data-stu-id="7452e-106">The tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="7452e-107">不用 30 分鐘，您就會獲得一個使用多個 Azure 資源，於雲端上啟動並執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7452e-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in the cloud.</span></span>

<span data-ttu-id="7452e-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="7452e-108">You will learn:</span></span>

* <span data-ttu-id="7452e-109">如何建立 Web 服務或調整現有的 Web 服務，以供 Web 方案使用。</span><span class="sxs-lookup"><span data-stu-id="7452e-109">How to create or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="7452e-110">如何使用 Azure WCF 轉送服務，在 Azure 應用程式與在其他位置裝載的 Web 服務之間共用資料。</span><span class="sxs-lookup"><span data-stu-id="7452e-110">How to use the Azure WCF Relay service to share data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="7452e-111">Azure 轉送如何透過混合式解決方案提供協助</span><span class="sxs-lookup"><span data-stu-id="7452e-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="7452e-112">商業方案通常由下列項目組成：為了應付全新的獨特商業需求而撰寫的自訂程式碼，以及既有方案和系統提供的現有功能。</span><span class="sxs-lookup"><span data-stu-id="7452e-112">Business solutions are typically composed of a combination of custom code written to tackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="7452e-113">眾多方案架構爭相開始使用雲端，以期能夠更輕鬆地處理擴充需求並降低操作成本。</span><span class="sxs-lookup"><span data-stu-id="7452e-113">Solution architects are starting to use the cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="7452e-114">在這麼做之後，它們發現想要運用做為其方案建置組塊的現有服務資產是在公司防火牆內，無法供雲端方案輕易存取。</span><span class="sxs-lookup"><span data-stu-id="7452e-114">In doing so, they find that existing service assets they'd like to leverage as building blocks for their solutions are inside the corporate firewall and out of easy reach for access by the cloud solution.</span></span> <span data-ttu-id="7452e-115">許多內部服務並不是以可輕易在公司網路邊緣公開的方式建置或主控。</span><span class="sxs-lookup"><span data-stu-id="7452e-115">Many internal services are not built or hosted in a way that they can be easily exposed at the corporate network edge.</span></span>

<span data-ttu-id="7452e-116">[Azure 轉送](https://azure.microsoft.com/services/service-bus/)是針對採取現有 Windows Communication Foundation (WCF) Web 服務，並使那些服務可供公司周邊外之解決方案安全存取的使用案例而設計，不需要進行會干擾公司網路基礎結構的變更。</span><span class="sxs-lookup"><span data-stu-id="7452e-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for the use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible to solutions that reside outside the corporate perimeter without requiring intrusive changes to the corporate network infrastructure.</span></span> <span data-ttu-id="7452e-117">此類轉送服務仍然裝載在其現有環境，但它們會將接聽連入工作階段和要求的工作委派給雲端裝載的轉送服務。</span><span class="sxs-lookup"><span data-stu-id="7452e-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests to the cloud-hosted relay service.</span></span> <span data-ttu-id="7452e-118">Azure 轉送也可使用[共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md) 驗證，保護那些服務免受未經授權的存取。</span><span class="sxs-lookup"><span data-stu-id="7452e-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="7452e-119">解決方案案例</span><span class="sxs-lookup"><span data-stu-id="7452e-119">Solution scenario</span></span>
<span data-ttu-id="7452e-120">在本教學課程中，您將建立 ASP.NET 網站，讓您可在產品庫存頁面上看到產品清單。</span><span class="sxs-lookup"><span data-stu-id="7452e-120">In this tutorial, you will create an ASP.NET website that enables you to see a list of products on the product inventory page.</span></span>

![][0]

<span data-ttu-id="7452e-121">此教學課程假設您有現有內部部署系統中的產品資訊，並使用 Azure 轉送來連接該系統。</span><span class="sxs-lookup"><span data-stu-id="7452e-121">The tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay to reach into that system.</span></span> <span data-ttu-id="7452e-122">這項模擬是由簡單主控台應用程式中執行的 Web 服務來進行，並由記憶體內的產品集支援。</span><span class="sxs-lookup"><span data-stu-id="7452e-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="7452e-123">您將能夠在自己的電腦上執行這個主控台應用程式，並將 Web 角色部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7452e-123">You will be able to run this console application on your own computer and deploy the web role into Azure.</span></span> <span data-ttu-id="7452e-124">在這麼做之後，您將看到在 Azure 資料中心執行的 Web 角色將確實呼叫至電腦，即使電腦幾乎確定會位於至少一個防火牆和網路位址轉譯 (NAT) 層後面也一樣。</span><span class="sxs-lookup"><span data-stu-id="7452e-124">By doing so, you will see how the web role running in the Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="7452e-125">設定開發環境</span><span class="sxs-lookup"><span data-stu-id="7452e-125">Set up the development environment</span></span>

<span data-ttu-id="7452e-126">開始開發 Azure 應用程式之前，請先下載工具並設定開發環境：</span><span class="sxs-lookup"><span data-stu-id="7452e-126">Before you can begin developing Azure applications, download the tools and set up your development environment:</span></span>

1. <span data-ttu-id="7452e-127">從 SDK [下載頁面](https://azure.microsoft.com/downloads/)安裝 Azure SDK for .NET。</span><span class="sxs-lookup"><span data-stu-id="7452e-127">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="7452e-128">在 **.NET** 資料行中，按一下您所使用的 [Visual Studio](http://www.visualstudio.com) 版本。</span><span class="sxs-lookup"><span data-stu-id="7452e-128">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="7452e-129">本教學課程中的步驟使用 Visual Studio 2015，但也可使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="7452e-129">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="7452e-130">當系統提示您執行或儲存安裝程式時，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="7452e-130">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="7452e-131">在 **Web Platform Installer** 中，按一下 [安裝] 並繼續進行安裝。</span><span class="sxs-lookup"><span data-stu-id="7452e-131">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="7452e-132">完成安裝後，您將具有開始進行開發所需的一切。</span><span class="sxs-lookup"><span data-stu-id="7452e-132">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="7452e-133">SDK 包含可讓您在 Visual Studio 輕易開發 Azure 應用程式的工具。</span><span class="sxs-lookup"><span data-stu-id="7452e-133">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="7452e-134">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="7452e-134">Create a namespace</span></span>

<span data-ttu-id="7452e-135">若要開始在 Azure 中使用轉送功能，首先必須建立服務命名空間。</span><span class="sxs-lookup"><span data-stu-id="7452e-135">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="7452e-136">命名空間提供範圍容器，可在應用程式內進行 Azure 資源定址。</span><span class="sxs-lookup"><span data-stu-id="7452e-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="7452e-137">請依照[此處的指示](relay-create-namespace-portal.md)來建立轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="7452e-137">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="7452e-138">建立內部部署伺服器</span><span class="sxs-lookup"><span data-stu-id="7452e-138">Create an on-premises server</span></span>

<span data-ttu-id="7452e-139">首先，您將建置 (模擬) 內部部署產品目錄系統。</span><span class="sxs-lookup"><span data-stu-id="7452e-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="7452e-140">此作業相當簡單；您可將它看成是呈現實際內部部署產品目錄系統，此系統具有我們正在嘗試整合的完整服務面。</span><span class="sxs-lookup"><span data-stu-id="7452e-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying to integrate.</span></span>

<span data-ttu-id="7452e-141">此專案是 Visual Studio 主控台應用程式，會使用 [Azure 服務匯流排 NuGet 套件](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)來納入服務匯流排程式庫和組態設定。</span><span class="sxs-lookup"><span data-stu-id="7452e-141">This project is a Visual Studio console application, and uses the [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) to include the Service Bus libraries and configuration settings.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="7452e-142">建立專案</span><span class="sxs-lookup"><span data-stu-id="7452e-142">Create the project</span></span>

1. <span data-ttu-id="7452e-143">使用系統管理員權限，啟動 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7452e-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="7452e-144">若要這樣做，請以滑鼠右鍵按一下 Visual Studio 程式圖示，然後按一下 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="7452e-144">To do so, right-click the Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="7452e-145">在 Visual Studio 的 [檔案] 功能表，按一下 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="7452e-145">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="7452e-146">從 [已安裝的範本] 的 [Visual C#] 下，按一下 [主控台應用程式 (.NET Framework]。</span><span class="sxs-lookup"><span data-stu-id="7452e-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="7452e-147">在 [名稱] 方塊中，鍵入名稱 **ProductsServer**：</span><span class="sxs-lookup"><span data-stu-id="7452e-147">In the **Name** box, type the name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="7452e-148">按一下 [確定] 以建立 **ProductsServer** 專案。</span><span class="sxs-lookup"><span data-stu-id="7452e-148">Click **OK** to create the **ProductsServer** project.</span></span>
5. <span data-ttu-id="7452e-149">如果已安裝 Visual Studio 的 NuGet 套件管理員，請跳至下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="7452e-149">If you have already installed the NuGet package manager for Visual Studio, skip to the next step.</span></span> <span data-ttu-id="7452e-150">否則，請造訪 [NuGet][NuGet]，然後按一下[安裝 NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)。</span><span class="sxs-lookup"><span data-stu-id="7452e-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="7452e-151">按照提示安裝 NuGet 套件管理員，然後重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7452e-151">Follow the prompts to install the NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="7452e-152">在 [方案總管] 中，以滑鼠右鍵按一下 **ProductsServer** 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="7452e-152">In Solution Explorer, right-click the **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="7452e-153">按一下 [瀏覽] 索引標籤，然後搜尋 `Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="7452e-153">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="7452e-154">選取 [WindowsAzure.ServiceBus] 套件。</span><span class="sxs-lookup"><span data-stu-id="7452e-154">Select the **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="7452e-155">按一下 [安裝] 並接受使用條款。</span><span class="sxs-lookup"><span data-stu-id="7452e-155">Click **Install**, and accept the terms of use.</span></span>

   ![][13]

   <span data-ttu-id="7452e-156">請注意，現在會參考必要的用戶端組件。</span><span class="sxs-lookup"><span data-stu-id="7452e-156">Note that the required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="7452e-157">新增產品連絡人的新類別。</span><span class="sxs-lookup"><span data-stu-id="7452e-157">Add a new class for your product contract.</span></span> <span data-ttu-id="7452e-158">在 [方案總管] 的 **ProductsServer** 專案上按一下滑鼠右鍵、按一下 [新增]，然後按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="7452e-158">In Solution Explorer, right-click the **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="7452e-159">在 [名稱] 方塊中，鍵入名稱 **ProductsContract.cs**。</span><span class="sxs-lookup"><span data-stu-id="7452e-159">In the **Name** box, type the name **ProductsContract.cs**.</span></span> <span data-ttu-id="7452e-160">然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="7452e-160">Then click **Add**.</span></span>
10. <span data-ttu-id="7452e-161">在 **ProductsContract.cs** 中，將命名空間定義取代為下列程式碼，以定義服務的連絡人。</span><span class="sxs-lookup"><span data-stu-id="7452e-161">In **ProductsContract.cs**, replace the namespace definition with the following code, which defines the contract for the service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define the data contract for the service
        [DataContract]
        // Declare the serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define the service contract.
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
11. <span data-ttu-id="7452e-162">在 Program.cs 中，將命名空間定義取代為下列程式碼，為它新增設定檔服務和主機。</span><span class="sxs-lookup"><span data-stu-id="7452e-162">In Program.cs, replace the namespace definition with the following code, which adds the profile service and the host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement the IProducts interface.
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

            // Display a message in the service console application
            // when the list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define the Main() function in the service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER to close");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="7452e-163">在 [方案總管] 中，按兩下 **App.config** 檔案，以在 Visual Studio 編輯器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="7452e-163">In Solution Explorer, double-click the **App.config** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="7452e-164">在 `<system.ServiceModel>` 元素底部 (但仍在 `<system.ServiceModel>` 內)，新增以下 XML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7452e-164">At the bottom of the `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add the following XML code.</span></span> <span data-ttu-id="7452e-165">請務必以您的命名空間名稱取代 yourServiceNamespace，並以您先前從入口網站擷取到的 SAS 金鑰取代 yourKey：</span><span class="sxs-lookup"><span data-stu-id="7452e-165">Be sure to replace *yourServiceNamespace* with the name of your namespace, and *yourKey* with the SAS key you retrieved earlier from the portal:</span></span>

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
13. <span data-ttu-id="7452e-166">仍是在 App.config 中，請以您先前從入口網站取得的連接字串來取代 `<appSettings>` 元素中的連接字串值。</span><span class="sxs-lookup"><span data-stu-id="7452e-166">Still in App.config, in the `<appSettings>` element, replace the connection string value with the connection string you previously obtained from the portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="7452e-167">按 **Ctrl+Shift+B**，或從 [建置] 功能表中按一下 [建置方案] 來建置應用程式並驗證您的工作到目前為止是否正確無誤。</span><span class="sxs-lookup"><span data-stu-id="7452e-167">Press **Ctrl+Shift+B** or from the **Build** menu, click **Build Solution** to build the application and verify the accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="7452e-168">建立 ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="7452e-168">Create an ASP.NET application</span></span>

<span data-ttu-id="7452e-169">在本節中，您將建置簡單的 ASP.NET 應用程式，來顯示從產品服務擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="7452e-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="7452e-170">建立專案</span><span class="sxs-lookup"><span data-stu-id="7452e-170">Create the project</span></span>

1. <span data-ttu-id="7452e-171">確定 Visual Studio 是以系統管理員權限來執行。</span><span class="sxs-lookup"><span data-stu-id="7452e-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="7452e-172">在 Visual Studio 的 [檔案] 功能表，按一下 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="7452e-172">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="7452e-173">從 [已安裝的範本] 的 [Visual C#] 下，按一下 [ASP.NET Web 應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="7452e-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="7452e-174">將專案命名為 **ProductsPortal**。</span><span class="sxs-lookup"><span data-stu-id="7452e-174">Name the project **ProductsPortal**.</span></span> <span data-ttu-id="7452e-175">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7452e-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="7452e-176">在 [新增 ASP.NET Web 應用程式] 對話方塊的 [ASP.NET 範本] 清單中，按一下 [MVC]。</span><span class="sxs-lookup"><span data-stu-id="7452e-176">From the **ASP.NET Templates** list in the **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="7452e-177">按一下 [變更驗證] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7452e-177">Click the **Change Authentication** button.</span></span> <span data-ttu-id="7452e-178">在 [變更驗證] 對話方塊中，確定已選取 [不需要驗證]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7452e-178">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="7452e-179">在本教學課程中，您會部署不需要使用者登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7452e-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="7452e-180">回到 [新增 ASP.NET Web 應用程式] 對話方塊，按一下 [確定] 以建立 MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7452e-180">Back in the **New ASP.NET Web Application** dialog, click **OK** to create the MVC app.</span></span>
8. <span data-ttu-id="7452e-181">您現在必須設定新 Web 應用程式的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="7452e-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="7452e-182">完成[本文的「發佈至 Azure」一節](../app-service-web/app-service-web-get-started-dotnet.md)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="7452e-182">Follow the steps in the [Publish to Azure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="7452e-183">然後，回到本教學課程並繼續進行下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="7452e-183">Then, return to this tutorial and proceed to the next step.</span></span>
10. <span data-ttu-id="7452e-184">在 [方案總管] 中，於 [模型] 上按一下滑鼠右鍵、按一下 [新增]，再按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="7452e-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="7452e-185">在 [名稱] 方塊中，鍵入名稱 **Product.cs**。</span><span class="sxs-lookup"><span data-stu-id="7452e-185">In the **Name** box, type the name **Product.cs**.</span></span> <span data-ttu-id="7452e-186">然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="7452e-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-the-web-application"></a><span data-ttu-id="7452e-187">修改 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7452e-187">Modify the web application</span></span>

1. <span data-ttu-id="7452e-188">在 Visual Studio 的 Product.cs 檔案中，將現有的命名空間定義取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="7452e-188">In the Product.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span>

   ```csharp
    // Declare properties for the products inventory.
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
2. <span data-ttu-id="7452e-189">在 [方案總管] 中展開 **Controllers** 資料夾，然後按兩下 **HomeController.cs** 檔案以在 Visual Studio 中開啟。</span><span class="sxs-lookup"><span data-stu-id="7452e-189">In Solution Explorer, expand the **Controllers** folder, then double-click the **HomeController.cs** file to open it in Visual Studio.</span></span>
3. <span data-ttu-id="7452e-190">在 **HomeController.cs** 檔案中，以下列程式碼取代現有的命名空間定義。</span><span class="sxs-lookup"><span data-stu-id="7452e-190">In **HomeController.cs**, replace the existing namespace definition with the following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of the products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="7452e-191">在 [方案總管] 中，展開 Views\Shared 資料夾，然後按兩下 **_Layout.cshtml** 檔案以在 Visual Studio 編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="7452e-191">In Solution Explorer, expand the Views\Shared folder, then double-click **_Layout.cshtml** to open it in the Visual Studio editor.</span></span>
5. <span data-ttu-id="7452e-192">將所有出現的 **My ASP.NET Application** 變更為 **LITWARE's Products**。</span><span class="sxs-lookup"><span data-stu-id="7452e-192">Change all occurrences of **My ASP.NET Application** to **LITWARE's Products**.</span></span>
6. <span data-ttu-id="7452e-193">移除 [首頁]、[關於] 和 [連絡人] 連結。</span><span class="sxs-lookup"><span data-stu-id="7452e-193">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="7452e-194">在下列範例中，刪除反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7452e-194">In the following example, delete the highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="7452e-195">在 [方案總管] 中，展開 Views\Home 資料夾，然後按兩下 **Index.cshtml** 以在 Visual Studio 編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="7452e-195">In Solution Explorer, expand the Views\Home folder, then double-click **Index.cshtml** to open it in the Visual Studio editor.</span></span> <span data-ttu-id="7452e-196">將檔案的整個內容取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="7452e-196">Replace the entire contents of the file with the following code.</span></span>

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
8. <span data-ttu-id="7452e-197">若要驗證您的工作到目前為止是否正確無誤，您可以按 **Ctrl+Shift+B** 來建置專案。</span><span class="sxs-lookup"><span data-stu-id="7452e-197">To verify the accuracy of your work so far, you can press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="run-the-app-locally"></a><span data-ttu-id="7452e-198">在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="7452e-198">Run the app locally</span></span>

<span data-ttu-id="7452e-199">執行應用程式以驗證它是否能正常運作。</span><span class="sxs-lookup"><span data-stu-id="7452e-199">Run the application to verify that it works.</span></span>

1. <span data-ttu-id="7452e-200">確定 **ProductsPortal** 為作用中專案。</span><span class="sxs-lookup"><span data-stu-id="7452e-200">Ensure that **ProductsPortal** is the active project.</span></span> <span data-ttu-id="7452e-201">在 [方案總管] 的專案名稱上按一下滑鼠右鍵，然後選取 [設定為啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="7452e-201">Right-click the project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="7452e-202">在 Visual Studio 中按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="7452e-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="7452e-203">您的應用程式應該就會出現在瀏覽器中並正在執行。</span><span class="sxs-lookup"><span data-stu-id="7452e-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-the-pieces-together"></a><span data-ttu-id="7452e-204">組合在一起</span><span class="sxs-lookup"><span data-stu-id="7452e-204">Put the pieces together</span></span>

<span data-ttu-id="7452e-205">下一步是利用 ASP.NET 應用程式連接內部部署產品伺服器。</span><span class="sxs-lookup"><span data-stu-id="7452e-205">The next step is to hook up the on-premises products server with the ASP.NET application.</span></span>

1. <span data-ttu-id="7452e-206">請在 Visual Studio 重新開啟您在[建立 ASP.NET 應用程式](#create-an-aspnet-application)一節中建立的 **ProductsPortal** 專案 (如果尚未開啟)。</span><span class="sxs-lookup"><span data-stu-id="7452e-206">If it is not already open, in Visual Studio re-open the **ProductsPortal** project you created in the [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="7452e-207">類似於＜建立內部部署伺服器＞一節中的步驟，將 NuGet 套件新增至專案參考。</span><span class="sxs-lookup"><span data-stu-id="7452e-207">Similar to the step in the "Create an On-Premises Server" section, add the NuGet package to the project references.</span></span> <span data-ttu-id="7452e-208">在 [方案總管] 中，以滑鼠右鍵按一下 **ProductsPortal** 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="7452e-208">In Solution Explorer, right-click the **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="7452e-209">搜尋「服務匯流排」並選取 [WindowsAzure.ServiceBus] 項目。</span><span class="sxs-lookup"><span data-stu-id="7452e-209">Search for "Service Bus" and select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="7452e-210">然後完成安裝並關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7452e-210">Then complete the installation and close this dialog box.</span></span>
4. <span data-ttu-id="7452e-211">在 [方案總管] 的 **ProductsPortal** 專案上按一下滑鼠右鍵，再按一下 [新增]，然後按一下 [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="7452e-211">In Solution Explorer, right-click the **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="7452e-212">從 **ProductsServer** 主控台專案導覽至 **ProductsContract.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="7452e-212">Navigate to the **ProductsContract.cs** file from the **ProductsServer** console project.</span></span> <span data-ttu-id="7452e-213">按一下以反白顯示 ProductsContract.cs。</span><span class="sxs-lookup"><span data-stu-id="7452e-213">Click to highlight ProductsContract.cs.</span></span> <span data-ttu-id="7452e-214">按一下 [新增] 旁邊的向下箭頭，然後按一下 [新增做為連結]。</span><span class="sxs-lookup"><span data-stu-id="7452e-214">Click the down arrow next to **Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="7452e-215">現在會在 Visual Studio 編輯器中開啟 **HomeController.cs** 檔案，並將命名空間定義取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="7452e-215">Now open the **HomeController.cs** file in the Visual Studio editor and replace the namespace definition with the following code.</span></span> <span data-ttu-id="7452e-216">請務必以服務命名空間名稱取代 *yourServiceNamespace*，並以 SAS 金鑰取代 *yourKey*。</span><span class="sxs-lookup"><span data-stu-id="7452e-216">Be sure to replace *yourServiceNamespace* with the name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="7452e-217">這可讓用戶端呼叫內部部署服務，並傳回呼叫結果。</span><span class="sxs-lookup"><span data-stu-id="7452e-217">This will enable the client to call the on-premises service, returning the result of the call.</span></span>

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
           // Declare the channel factory.
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
                   // Return a view of the products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="7452e-218">在 [方案總管] 中，以滑鼠右鍵按一下 **ProductsPortal** 方案 (務必以滑鼠右鍵按一下方案，而非專案)。</span><span class="sxs-lookup"><span data-stu-id="7452e-218">In Solution Explorer, right-click the **ProductsPortal** solution (make sure to right-click the solution, not the project).</span></span> <span data-ttu-id="7452e-219">按一下 [新增]，然後按一下 [現有專案]。</span><span class="sxs-lookup"><span data-stu-id="7452e-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="7452e-220">導覽至 **ProductsServer** 專案，然後按兩下 **ProductsServer.csproj** 方案檔來新增它。</span><span class="sxs-lookup"><span data-stu-id="7452e-220">Navigate to the **ProductsServer** project, then double-click the **ProductsServer.csproj** solution file to add it.</span></span>
9. <span data-ttu-id="7452e-221">**ProductsServer** 必須在執行中，才能在 **ProductsPortal** 上顯示資料。</span><span class="sxs-lookup"><span data-stu-id="7452e-221">**ProductsServer** must be running in order to display the data on **ProductsPortal**.</span></span> <span data-ttu-id="7452e-222">在 [方案總管] 的 **ProductsPortal** 方案上按一下滑鼠右鍵，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="7452e-222">In Solution Explorer, right-click the **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="7452e-223">[屬性頁面] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7452e-223">The **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="7452e-224">在左側，按一下 [啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="7452e-224">On the left side, click **Startup Project**.</span></span> <span data-ttu-id="7452e-225">在右側，按一下 [多個啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="7452e-225">On the right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="7452e-226">確定 **ProductsServer** 和 **ProductsPortal** 依序出現，且 [啟動] 設為兩者的動作。</span><span class="sxs-lookup"><span data-stu-id="7452e-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as the action for both.</span></span>

      ![][25]

11. <span data-ttu-id="7452e-227">仍是在 [屬性] 對話方塊中，按一下左側的 [專案相依性]。</span><span class="sxs-lookup"><span data-stu-id="7452e-227">Still in the **Properties** dialog box, click **Project Dependencies** on the left side.</span></span>
12. <span data-ttu-id="7452e-228">在 [專案] 清單中，按一下 **ProductsServer**。</span><span class="sxs-lookup"><span data-stu-id="7452e-228">In the **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="7452e-229">確定未選取 [ProductsPortal]。</span><span class="sxs-lookup"><span data-stu-id="7452e-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="7452e-230">在 [專案] 清單中，按一下 **ProductsPortal**。</span><span class="sxs-lookup"><span data-stu-id="7452e-230">In the **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="7452e-231">確定已選取 [ProductsServer]。</span><span class="sxs-lookup"><span data-stu-id="7452e-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="7452e-232">按一下 [屬性頁面] 對話方塊中的 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7452e-232">Click **OK** in the **Property Pages** dialog box.</span></span>

## <a name="run-the-project-locally"></a><span data-ttu-id="7452e-233">在本機執行專案</span><span class="sxs-lookup"><span data-stu-id="7452e-233">Run the project locally</span></span>

<span data-ttu-id="7452e-234">若要在本機測試應用程式，請在 Visual Studio 中按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="7452e-234">To test the application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="7452e-235">內部部署伺服器 (**ProductsServer**) 應該會先啟動，然後 **ProductsPortal** 應用程式應在瀏覽器視窗中啟動。</span><span class="sxs-lookup"><span data-stu-id="7452e-235">The on-premises server (**ProductsServer**) should start first, then the **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="7452e-236">此時，您將看到從產品服務內部部署系統擷取的產品庫存清單資料。</span><span class="sxs-lookup"><span data-stu-id="7452e-236">This time, you will see that the product inventory lists data retrieved from the product service on-premises system.</span></span>

![][10]

<span data-ttu-id="7452e-237">按 **ProductsPortal** 頁面上的 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="7452e-237">Press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="7452e-238">每次重新整理頁面時，您會看到伺服器應用程式在呼叫來自 **ProductsServer** 的 `GetProducts()` 時顯示一則訊息。</span><span class="sxs-lookup"><span data-stu-id="7452e-238">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="7452e-239">先關閉這兩個應用程式，才能繼續下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="7452e-239">Close both applications before proceeding to the next step.</span></span>

## <a name="deploy-the-productsportal-project-to-an-azure-web-app"></a><span data-ttu-id="7452e-240">將 ProductsPortal 專案部署至 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7452e-240">Deploy the ProductsPortal project to an Azure web app</span></span>

<span data-ttu-id="7452e-241">下一個步驟是重新發佈 Azure Web 應用程式 **ProductsPortal** 前端。</span><span class="sxs-lookup"><span data-stu-id="7452e-241">The next step is to republish the Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="7452e-242">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="7452e-242">Do the following:</span></span>

1. <span data-ttu-id="7452e-243">在 [方案總管] 中，於 **ProductsPortal** 專案上按一下滑鼠右鍵，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="7452e-243">In Solution Explorer, right-click the **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="7452e-244">然後，按一下 [發佈] 頁面上的 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="7452e-244">Then, click **Publish** on the **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7452e-245">在部署後自動啟動 **ProductsPortal** Web 專案時，您可在瀏覽器視窗中看到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7452e-245">You may see an error message in the browser window when the **ProductsPortal** web project is automatically launched after the deployment.</span></span> <span data-ttu-id="7452e-246">這是預期的，且因為 **ProductsServer** 應用程式尚未執行而出現。</span><span class="sxs-lookup"><span data-stu-id="7452e-246">This is expected, and occurs because the **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="7452e-247">請複製已部署 Web 應用程式的 URL，印為您在下一個步驟中需要用到 URL。</span><span class="sxs-lookup"><span data-stu-id="7452e-247">Copy the URL of the deployed web app, as you will need the URL in the next step.</span></span> <span data-ttu-id="7452e-248">您也可以從 Visual Studio 中的 [Azure App Service 活動] 視窗中取得此 URL：</span><span class="sxs-lookup"><span data-stu-id="7452e-248">You can also obtain this URL from the Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="7452e-249">關閉瀏覽器視窗以停止執行中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7452e-249">Close the browser window to stop the running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="7452e-250">將 ProductsPortal 設定為 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7452e-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="7452e-251">在雲端執行此應用程式之前，您必須確定 **ProductsPortal** 是從 Visual Studio 內以 Web 應用程式的形式啟動。</span><span class="sxs-lookup"><span data-stu-id="7452e-251">Before running the application in the cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="7452e-252">在 Visual Studio 中，以滑鼠右鍵按一下 **ProductsPortal** 專案，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="7452e-252">In Visual Studio, right-click the **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="7452e-253">在左側欄中，按一下 [Web]。</span><span class="sxs-lookup"><span data-stu-id="7452e-253">In the left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="7452e-254">在 [起始動作] 區段中，按一下 [起始 URL] 按鈕，然後在文字方塊中輸入您先前部署的 Web 應用程式的 URL，例如 `http://productsportal1234567890.azurewebsites.net/`。</span><span class="sxs-lookup"><span data-stu-id="7452e-254">In the **Start Action** section, click the **Start URL** button, and in the text box enter the URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="7452e-255">從 Visual Studio 的 [檔案] 功能表中，按一下 [全部儲存]。</span><span class="sxs-lookup"><span data-stu-id="7452e-255">From the **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="7452e-256">在 Visual Studio 的 [建置] 功能表中，按一下 [重建方案]。</span><span class="sxs-lookup"><span data-stu-id="7452e-256">From the Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="7452e-257">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="7452e-257">Run the application</span></span>

1. <span data-ttu-id="7452e-258">按 F5 以建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="7452e-258">Press F5 to build and run the application.</span></span> <span data-ttu-id="7452e-259">內部部署伺服器 (**ProductsServer** 主控台應用程式) 應該會第一個啟動，然後 **ProductsPortal** 應用程式應該會在瀏覽器視窗中啟動，如下面的螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="7452e-259">The on-premises server (the **ProductsServer** console application) should start first, then the **ProductsPortal** application should start in a browser window, as shown in the following screen shot.</span></span> <span data-ttu-id="7452e-260">再次注意，產品庫存清單會列出從產品服務內部部署系統擷取的資料，並在 Web 應用程式中顯示該資訊。</span><span class="sxs-lookup"><span data-stu-id="7452e-260">Notice again that the product inventory lists data retrieved from the product service on-premises system, and displays that data in the web app.</span></span> <span data-ttu-id="7452e-261">檢查 URL，確定 **ProductsPortal** 正在雲端中以 Azure Web 應用程式的形式執行。</span><span class="sxs-lookup"><span data-stu-id="7452e-261">Check the URL to make sure that **ProductsPortal** is running in the cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="7452e-262">**ProductsServer** 主控台應用程式必須正在執行中，而且能夠提供資料給 **ProductsPortal** 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7452e-262">The **ProductsServer** console application must be running and able to serve the data to the **ProductsPortal** application.</span></span> <span data-ttu-id="7452e-263">如果瀏覽器顯示錯誤，請等候幾秒，讓 **ProductsServer** 載入並顯示下列訊息。</span><span class="sxs-lookup"><span data-stu-id="7452e-263">If the browser displays an error, wait a few more seconds for **ProductsServer** to load and display the following message.</span></span> <span data-ttu-id="7452e-264">然後按瀏覽器中的 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="7452e-264">Then press **Refresh** in the browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="7452e-265">回到瀏覽器中，按 **ProductsPortal** 頁面上的 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="7452e-265">Back in the browser, press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="7452e-266">每次重新整理頁面時，您會看到伺服器應用程式在呼叫來自 **ProductsServer** 的 `GetProducts()` 時顯示一則訊息。</span><span class="sxs-lookup"><span data-stu-id="7452e-266">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="7452e-267">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7452e-267">Next steps</span></span>

<span data-ttu-id="7452e-268">若要深入了解 Azure 轉送，請參閱下列資源︰</span><span class="sxs-lookup"><span data-stu-id="7452e-268">To learn more about Azure Relay, see the following resources:</span></span>  

* [<span data-ttu-id="7452e-269">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="7452e-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="7452e-270">如何使用轉送</span><span class="sxs-lookup"><span data-stu-id="7452e-270">How to use Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
