---
title: "使用 Azure 轉送的服務匯流排 REST 教學課程 |Microsoft Docs"
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
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="3e4b9-103">Azure WCF 轉送的 REST 教學課程</span><span class="sxs-lookup"><span data-stu-id="3e4b9-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="3e4b9-104">本教學課程描述如何建置簡單的 Azure 轉送主機應用程式來公開 REST 架構介面。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="3e4b9-105">REST 可讓 Web 用戶端 (例如 Web 瀏覽器) 透過 HTTP 要求存取服務匯流排 API。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="3e4b9-106">本教學課程會使用 Windows Communication Foundation (WCF) REST 程式設計模型，在服務匯流排上建構 REST 服務。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="3e4b9-107">如需詳細資訊，請參閱 WCF 文件中的 [WCF REST 程式設計模型](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model)和[設計與實作服務](/dotnet/framework/wcf/designing-and-implementing-services)。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="3e4b9-108">步驟 1：建立命名空間</span><span class="sxs-lookup"><span data-stu-id="3e4b9-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="3e4b9-109">若要開始在 Azure 中使用轉送功能，首先必須建立服務命名空間。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="3e4b9-110">命名空間提供範圍容器，可在應用程式內進行 Azure 資源定址。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="3e4b9-111">請依照[此處的指示](relay-create-namespace-portal.md)來建立轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="3e4b9-112">步驟 2：定義 REST 架構的 WCF 服務合約以與 Azure 轉送搭配使用</span><span class="sxs-lookup"><span data-stu-id="3e4b9-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="3e4b9-113">當您建立 WCF REST 樣式服務時，必須定義合約。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="3e4b9-114">合約會指定主機支援哪些作業。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="3e4b9-115">服務作業可視為 Web 服務方法。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="3e4b9-116">合約可以透過定義 C++、C# 或 Visual Basic 介面建立。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="3e4b9-117">介面中的每個方法會對應一個特定服務作業。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="3e4b9-118">[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 屬性必須套用至每個介面，且 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 屬性必須套用至每個作業。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="3e4b9-119">如果介面中的方法具備沒有 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 的 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)，則不會公開該方法。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="3e4b9-120">用來執行這些工作的程式碼顯示在程序後面的範例中。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="3e4b9-121">WCF 合約與 REST 樣式合約之間的主要差異在於屬性會新增至 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx)：[WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="3e4b9-122">這個屬性可讓您將介面的方法對應至介面另一端的方法。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="3e4b9-123">在此情況下，我們會使用 [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) 將方法連結至 HTTP GET。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="3e4b9-124">這可讓服務匯流排準確擷取和解譯傳送到介面的命令。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="3e4b9-125">使用介面建立合約</span><span class="sxs-lookup"><span data-stu-id="3e4b9-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="3e4b9-126">以系統管理員身分開啟 Visual Studio：以滑鼠右鍵按一下 [開始] 功能表中的程式，然後按一下 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="3e4b9-127">這會建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-127">Create a new console application project.</span></span> <span data-ttu-id="3e4b9-128">按一下 [檔案] 功能表，再依序選取 [新增] 及 [專案]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="3e4b9-129">在 [新增專案] 對話方塊中，按一下 [Visual C#]，選取 [主控台應用程式] 範本，並將它命名為 **ImageListener**。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="3e4b9-130">使用預設 [位置]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-130">Use the default **Location**.</span></span> <span data-ttu-id="3e4b9-131">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="3e4b9-132">若為 C# 專案，Visual Studio 會建立 `Program.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="3e4b9-133">這個類別包含空的 `Main()` 方法，即正確建置主控台應用程式專案所需的方法。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="3e4b9-134">安裝服務匯流排 NuGet 封裝，以將服務匯流排和 **System.ServiceModel.dll** 的參考新增至專案。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="3e4b9-135">此封裝會自動新增服務匯流排程式庫及 WCF **System.ServiceModel** 的參考。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="3e4b9-136">在 [方案總管] 中，以滑鼠右鍵按一下 **ImageListener** 專案，然後按一下 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="3e4b9-137">按一下 [瀏覽] 索引標籤，然後搜尋 `Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="3e4b9-138">按一下 [安裝] 並接受使用條款。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="3e4b9-139">您必須明確地將 **System.ServiceModel.dll** 的參考新增至專案：</span><span class="sxs-lookup"><span data-stu-id="3e4b9-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="3e4b9-140">a.</span><span class="sxs-lookup"><span data-stu-id="3e4b9-140">a.</span></span> <span data-ttu-id="3e4b9-141">在 [方案總管] 中，以滑鼠右鍵按一下專案資料夾下的**參考**資料夾，然後按一下 [加入參考]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="3e4b9-142">b.</span><span class="sxs-lookup"><span data-stu-id="3e4b9-142">b.</span></span> <span data-ttu-id="3e4b9-143">在 [新增參考] 對話方塊中，按一下左側的 [架構] 索引標籤，然後在 [搜尋] 方塊中輸入 **System.ServiceModel.Web**。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="3e4b9-144">選取 [System.ServiceModel.Web] 核取方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="3e4b9-145">在 Program.cs 檔案開頭處新增下列 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="3e4b9-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) 是可讓您以程式設計方式存取 WCF 基本功能的命名空間。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="3e4b9-147">WCF 轉送會使用 WCF 的許多物件和屬性來定義服務合約。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="3e4b9-148">您將在大部分轉送應用程式中使用此命名空間。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="3e4b9-149">同樣地，[System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) 可協助定義通道，您可透過此物件來與 Azure 轉送和用戶端 Web 瀏覽器通訊。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="3e4b9-150">最後，[System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) 包含可讓您建立 Web 架構應用程式的類型。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="3e4b9-151">將 `ImageListener` 命名空間重新命名為 **Microsoft.ServiceBus.Samples**。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="3e4b9-152">直接在命名空間宣告的左大括號後面定義名為 **IImageContract** 的新介面，並將 **ServiceContractAttribute** 屬性套用至介面，且值設為 `http://samples.microsoft.com/ServiceModel/Relay/`。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="3e4b9-153">命名空間值與您的整個程式碼範圍中使用的命名空間不同。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="3e4b9-154">命名空間值作為此合約的唯一識別碼，且應該具有版本資訊。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="3e4b9-155">如需詳細資訊，請參閱[服務版本設定](http://go.microsoft.com/fwlink/?LinkID=180498)。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="3e4b9-156">明確指定命名空間可避免將預設命名空間值新增至合約名稱。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="3e4b9-157">在 `IImageContract` 介面中，針對 `IImageContract` 合約在介面中公開的單一作業宣告方法，並將 `OperationContractAttribute` 屬性套用至您想要公開為公用服務匯流排合約一部分的方法。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="3e4b9-158">在 **OperationContract** 屬性中，新增 **WebGet** 值。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="3e4b9-159">這樣做可讓轉送服務將 HTTP GET 要求路由傳送至 `GetImage`，以及將 `GetImage` 的傳回值轉譯成 HTTP GETRESPONSE 回覆。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="3e4b9-160">稍後在教學課程中，您將使用 Web 瀏覽器來存取此方法，並可在瀏覽器中顯示映像。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="3e4b9-161">緊接著 `IImageContract` 定義後面，宣告從 `IImageContract` 和 `IClientChannel` 介面繼承的通道。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="3e4b9-162">通道是 WCF 物件，服務和用戶端可透過它彼此傳遞資訊。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="3e4b9-163">您稍後將在主機應用程式中建立通道。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="3e4b9-164">Azure 轉送接著會使用此通道，將 HTTP GET 要求從瀏覽器傳遞至您的 **GetImage** 實作。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="3e4b9-165">轉送也會使用通道來取得 **GetImage** 傳回值，並轉譯成用戶端瀏覽器的 HTTP GETRESPONSE。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="3e4b9-166">從 [建置] 功能表中，按一下 [建置方案] 以確認您的工作到目前為止是否正確無誤。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="3e4b9-167">範例</span><span class="sxs-lookup"><span data-stu-id="3e4b9-167">Example</span></span>
<span data-ttu-id="3e4b9-168">下列程式碼示範定義 WCF 轉送合約的基本介面。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="3e4b9-169">步驟 3：實作 REST 架構 WCF 服務合約以使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="3e4b9-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="3e4b9-170">建立 REST 樣式的 WCF 轉送服務需要先建立合約，您可使用介面定義該合約。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="3e4b9-171">下一步是實作介面。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-171">The next step is to implement the interface.</span></span> <span data-ttu-id="3e4b9-172">這牽涉到建立名為 **ImageService** 的類別，該類別實作使用者定義的 **IImageContract** 介面。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="3e4b9-173">實作合約後，接著可使用 App.config 檔案設定介面。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="3e4b9-174">組態檔包含應用程式的必要資訊，例如服務名稱、合約名稱，以及用來與轉送服務通訊的通訊協定類型。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="3e4b9-175">程序後面的範例提供用來執行這些工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="3e4b9-176">如同先前的步驟，實作 REST 樣式合約與 WCF 轉送合約之間的差異很小。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="3e4b9-177">實作 REST 樣式服務匯流排合約</span><span class="sxs-lookup"><span data-stu-id="3e4b9-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="3e4b9-178">緊接在 **IImageContract** 介面的定義之後，建立名為 **ImageService** 的新類別。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="3e4b9-179">**ImageService** 類別會實作 **IImageContract** 介面。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="3e4b9-180">類似於其他介面實作，您可以在不同的檔案中實作定義。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="3e4b9-181">不過，在此教學課程中，實作會出現在與介面定義和 `Main()` 方法相同的檔案中。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="3e4b9-182">將 [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) 屬性套用至 **IImageService** 類別，以表示此類別為 WCF 合約的實作。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="3e4b9-183">如先前所述，此命名空間不是傳統的命名空間。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="3e4b9-184">相反地，它是識別合約的 WCF 架構的一部分。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="3e4b9-185">如需詳細資訊，請參閱 WCF 文件中的[資料合約名稱](https://msdn.microsoft.com/library/ms731045.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="3e4b9-186">將 .jpg 映像加入至您的專案。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="3e4b9-187">這是此服務在接收瀏覽器中顯示的圖片。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="3e4b9-188">以滑鼠右鍵按一下您的專案，然後按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="3e4b9-189">然後按一下 [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-189">Then click **Existing Item**.</span></span> <span data-ttu-id="3e4b9-190">使用 [加入現有項目] 對話方塊瀏覽至適當的 .jpg，然後按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="3e4b9-191">加入檔案時，確定在 [檔案名稱:] 欄位旁的下拉式清單中選取 [所有檔案]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="3e4b9-192">本教學課程的其餘部分假設映像的名稱為 "image.jpg"。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="3e4b9-193">如果您有不同的檔案，您必須重新命名映像，或變更您的程式碼來彌補。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="3e4b9-194">為確定執行中的服務能夠找到此影像檔，請在 [方案總管] 中以滑鼠右鍵按一下該影像檔，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="3e4b9-195">在 [屬性] 窗格中，將 [複製到輸出目錄] 設為 [有更新時才複製]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="3e4b9-196">將 **System.Drawing.dll** 組件的參考新增至專案，並新增下列關聯的 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="3e4b9-197">在 **ImageService** 類別中，加入下列建構函式，以便載入點陣圖並準備將它傳送給用戶端瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
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
7. <span data-ttu-id="3e4b9-198">緊接先前的程式碼後方，在 **ImageService** 類別中加入下列 **GetImage** 方法，以傳回包含該影像的 HTTP 訊息。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
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
   
    <span data-ttu-id="3e4b9-199">這個實作會使用 **MemoryStream** 來擷取映像，並備妥它以串流至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="3e4b9-200">它會從零起算串流位置，將串流內容宣告為 jpeg，並且串流資訊。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="3e4b9-201">從 [建置] 功能表中，按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="3e4b9-202">為服務匯流排上執行的 Web 服務定義組態</span><span class="sxs-lookup"><span data-stu-id="3e4b9-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="3e4b9-203">在 [方案總管] 中按兩下 **App.config**，以在 Visual Studio 編輯器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="3e4b9-204">**App.config** 檔案包含服務名稱、端點 (也就是 Azure 轉送公開的位置，讓用戶端與主機能夠彼此通訊) 和繫結 (用於通訊的通訊協定類型)。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="3e4b9-205">此處的主要差異是設定的服務端點會參考 [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) 繫結。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="3e4b9-206">`<system.serviceModel>` XML 元素是定義一或多個服務的 WCF 元素。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="3e4b9-207">在這裡，它用來定義服務名稱和端點。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="3e4b9-208">在 `<system.serviceModel>` 元素底部 (但仍在 `<system.serviceModel>` 內)，新增具有以下內容的 `<bindings>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="3e4b9-209">這會定義應用程式中使用的繫結。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="3e4b9-210">您可以定義多個繫結，但在本教學課程中您只會定義一個。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="3e4b9-211">先前的程式碼會將 **relayClientAuthenticationType** 設為 **None** 來定義 WCF 轉送 [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) 繫結。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="3e4b9-212">這個設定表示使用此繫結的端點不需要用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="3e4b9-213">在 `<bindings>` 元素後方加入 `<services>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="3e4b9-214">類似於繫結，您可以在單一組態檔中定義多個服務。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="3e4b9-215">不過，您在本教學課程中只會定義一個。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="3e4b9-216">這個步驟會設定服務，該服務會使用先前定義的預設 **webHttpRelayBinding**。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="3e4b9-217">它也會使用在下一個步驟中定義的預設 **sbTokenProvider**。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="3e4b9-218">在 `<services>` 元素後，建立具有下列內容的 `<behaviors>` 元素，以您先前從 [Azure 入口網站][Azure portal]所取得的「共用存取簽章」(SAS) 金鑰來取代 "SAS_KEY"。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="3e4b9-219">仍是在 App.config 中，請以您先前從入口網站取得的連接字串，取代 `<appSettings>` 元素中的整個連接字串值。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="3e4b9-220">從 [建置] 功能表中，按一下 [建置方案] 以建置整個方案。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="3e4b9-221">範例</span><span class="sxs-lookup"><span data-stu-id="3e4b9-221">Example</span></span>
<span data-ttu-id="3e4b9-222">下列程式碼會顯示使用 **WebHttpRelayBinding** 繫結，正在服務匯流排上執行之 REST 架構服務的合約和服務實作。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="3e4b9-223">下列範例會顯示與服務相關聯的 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
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

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="3e4b9-224">步驟 4：裝載 REST 架構的 WCF 服務以使用 Azure 轉送</span><span class="sxs-lookup"><span data-stu-id="3e4b9-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="3e4b9-225">此步驟描述如何搭配 WCF 轉送使用主控台應用程式來執行 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="3e4b9-226">程序後面的範例提供此步驟中撰寫的完整程式碼清單。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="3e4b9-227">建立服務的基底位址</span><span class="sxs-lookup"><span data-stu-id="3e4b9-227">To create a base address for the service</span></span>
1. <span data-ttu-id="3e4b9-228">在 `Main()` 函式宣告中，建立變數來儲存專案的命名空間。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="3e4b9-229">務必以您先前建立的轉送命名空間名稱來取代 `yourNamespace`。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="3e4b9-230">服務匯流排會使用您的命名空間名稱來建立唯一 URI。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="3e4b9-231">為根據命名空間之服務的基底位址建立 `Uri` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="3e4b9-232">建立和設定 Web 服務主機</span><span class="sxs-lookup"><span data-stu-id="3e4b9-232">To create and configure the web service host</span></span>
* <span data-ttu-id="3e4b9-233">建立 Web 服務主機，使用本節稍早建立的 URI 位址。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="3e4b9-234">服務主機是具現化主機應用程式的 WCF 物件。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="3e4b9-235">此範例會將您要建立的主機類型 (**ImageService**)，及要公開主機應用程式的位址傳給它。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="3e4b9-236">執行 Web 服務主機</span><span class="sxs-lookup"><span data-stu-id="3e4b9-236">To run the web service host</span></span>
1. <span data-ttu-id="3e4b9-237">開啟服務。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="3e4b9-238">服務現在正在執行。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-238">The service is now running.</span></span>
2. <span data-ttu-id="3e4b9-239">顯示訊息，指出服務正在執行，以及如何停止服務。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="3e4b9-240">完成時，關閉服務主機。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="3e4b9-241">範例</span><span class="sxs-lookup"><span data-stu-id="3e4b9-241">Example</span></span>
<span data-ttu-id="3e4b9-242">下列範例包括教學課程先前步驟的服務合約和實作，以及在主控台應用程式中主控服務。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="3e4b9-243">將下列程式碼編譯為名為 ImageListener.exe 的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-243">Compile the following code into an executable named ImageListener.exe.</span></span>

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

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="3e4b9-244">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="3e4b9-244">Compiling the code</span></span>
<span data-ttu-id="3e4b9-245">建置解決方案後，請執行下列命令以執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="3e4b9-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="3e4b9-246">按 **F5**，或瀏覽至可執行檔的位置 (ImageListener\bin\Debug\ImageListener.exe) 來執行服務。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="3e4b9-247">讓應用程式保持執行狀態，因為需要它來執行下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="3e4b9-248">將位址從命令提示字元複製並貼到瀏覽器以查看映像。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="3e4b9-249">當您完成時，請在 [命令提示字元] 視窗中按 **Enter** 來關閉應用程式。</span><span class="sxs-lookup"><span data-stu-id="3e4b9-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e4b9-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e4b9-250">Next steps</span></span>
<span data-ttu-id="3e4b9-251">既然您已經建置使用服務匯流排轉送服務的應用程式，請參閱下列文章以進一步了解 Azure 轉送：</span><span class="sxs-lookup"><span data-stu-id="3e4b9-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="3e4b9-252">Azure 服務匯流排架構概觀</span><span class="sxs-lookup"><span data-stu-id="3e4b9-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="3e4b9-253">Azure 轉送概觀</span><span class="sxs-lookup"><span data-stu-id="3e4b9-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="3e4b9-254">如何使用 WCF 轉送服務搭配 .NET</span><span class="sxs-lookup"><span data-stu-id="3e4b9-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
