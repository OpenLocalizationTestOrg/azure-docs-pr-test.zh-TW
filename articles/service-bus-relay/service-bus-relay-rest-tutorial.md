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
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="d9c6d-103">Azure WCF 轉送的 REST 教學課程</span><span class="sxs-lookup"><span data-stu-id="d9c6d-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="d9c6d-104">本教學課程說明如何 toobuild 簡單的 Azure 轉送裝載以 REST 為基礎的介面公開 （expose） 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="d9c6d-105">其餘可讓 web 用戶端，例如網頁瀏覽器，透過 HTTP 的服務匯流排 Api 要求 tooaccess hello。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="d9c6d-106">hello 教學課程會使用服務匯流排上 hello Windows Communication Foundation (WCF) REST 程式設計模型 tooconstruct REST 服務。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="d9c6d-107">如需詳細資訊，請參閱[WCF REST 程式設計模型](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model)和[設計與實作服務](/dotnet/framework/wcf/designing-and-implementing-services)hello WCF 文件中。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="d9c6d-108">步驟 1：建立命名空間</span><span class="sxs-lookup"><span data-stu-id="d9c6d-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="d9c6d-109">使用 toobegin hello 轉送功能，在 Azure 中的，您必須先建立服務命名空間。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="d9c6d-110">命名空間提供範圍容器，可在應用程式內進行 Azure 資源定址。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="d9c6d-111">請遵循 hello[這裡的指示](relay-create-namespace-portal.md)toocreate 轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="d9c6d-112">步驟 2： 定義與 Azure 轉送的 REST 式 WCF 服務合約 toouse</span><span class="sxs-lookup"><span data-stu-id="d9c6d-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="d9c6d-113">當您建立 WCF rest 服務時，您必須定義 hello 合約。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="d9c6d-114">hello 合約會指定哪些作業 hello 主應用程式支援。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="d9c6d-115">服務作業可視為 Web 服務方法。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="d9c6d-116">合約可以透過定義 C++、C# 或 Visual Basic 介面建立。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="d9c6d-117">Hello 介面中的每個方法對應 tooa 特定服務作業。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="d9c6d-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)屬性必須套用的 tooeach 介面和 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx)屬性必須套用的 tooeach 作業。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="d9c6d-119">如果其中有 hello 的介面中的方法[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)沒有 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx)，未公開該方法。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="d9c6d-120">hello 用於這些工作的程式碼所示 hello hello 程序的範例。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="d9c6d-121">hello WCF 合約和 rest 式合約的主要差異是 hello 新增屬性 toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="d9c6d-122">此屬性可讓 hello 介面的另一端 toomap 上 hello 介面 tooa 方法中的方法。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="d9c6d-123">在此情況下，我們將使用[WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink 方法 tooHTTP GET。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="d9c6d-124">這可讓服務匯流排 tooaccurately 擷取和解譯傳送 toohello 介面的命令。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="d9c6d-125">toocreate 合約的介面</span><span class="sxs-lookup"><span data-stu-id="d9c6d-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="d9c6d-126">開啟 Visual Studio 以系統管理員： hello 中的以滑鼠右鍵按一下 hello 程式**啟動**功能表，然後再按一下**系統管理員身分執行**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="d9c6d-127">這會建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-127">Create a new console application project.</span></span> <span data-ttu-id="d9c6d-128">按一下 hello**檔案**功能表，然後選取**新增**，然後選取**專案**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="d9c6d-129">在 hello**新專案**對話方塊中，按一下**Visual C#**，選取 hello**主控台應用程式**範本，並將它命名**ImageListener**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="d9c6d-130">使用預設的 hello**位置**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-130">Use hello default **Location**.</span></span> <span data-ttu-id="d9c6d-131">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="d9c6d-132">若為 C# 專案，Visual Studio 會建立 `Program.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="d9c6d-133">這個類別包含空`Main()`正確主控台應用程式專案 toobuild 所需的方法。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="d9c6d-134">新增參考 tooService 匯流排和**System.ServiceModel.dll** toohello 專案藉由安裝 hello 服務匯流排 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="d9c6d-135">此套件會自動將參考 toohello 服務匯流排程式庫，以及 hello WCF **System.ServiceModel**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="d9c6d-136">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ImageListener**專案，然後再按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="d9c6d-137">按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="d9c6d-138">按一下**安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="d9c6d-139">您必須明確的加入的參考**System.ServiceModel.Web.dll** toohello 專案：</span><span class="sxs-lookup"><span data-stu-id="d9c6d-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="d9c6d-140">a.</span><span class="sxs-lookup"><span data-stu-id="d9c6d-140">a.</span></span> <span data-ttu-id="d9c6d-141">在 [方案總管] 中，以滑鼠右鍵按一下 hello**參考**下 hello 專案資料夾，然後按一下資料夾**加入參考**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="d9c6d-142">b.</span><span class="sxs-lookup"><span data-stu-id="d9c6d-142">b.</span></span> <span data-ttu-id="d9c6d-143">在 [hello**加入參考**對話方塊方塊中，按一下 hello **Framework** ] 索引標籤左側為 hello 和 hello**搜尋**方塊中，輸入**System.ServiceModel.Web**.</span><span class="sxs-lookup"><span data-stu-id="d9c6d-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="d9c6d-144">選取 hello **System.ServiceModel.Web**核取方塊，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="d9c6d-145">新增下列 hello`using`在 hello hello Program.cs 檔案最上方的陳述式。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="d9c6d-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx)是 hello 命名空間，可讓 WCF 以程式設計方式存取 toobasic 功能。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="d9c6d-147">許多 hello 物件和屬性的 toodefine WCF 服務合約，則會使用 WCF 轉送。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="d9c6d-148">您將在大部分轉送應用程式中使用此命名空間。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="d9c6d-149">同樣地， [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx)有助於定義 hello 通道，這是您與 Azure 轉送和 hello 的用戶端 web 瀏覽器透過此通訊的 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="d9c6d-150">最後， [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx)包含 hello toocreate web 應用程式可讓您的型別。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="d9c6d-151">重新命名 hello`ImageListener`命名空間太**Microsoft.ServiceBus.Samples**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="d9c6d-152">直接之後 hello 開啟 hello 命名空間宣告的大括號，定義名為的新介面**IImageContract**並套用 hello **ServiceContractAttribute**屬性 toohello 介面值`http://samples.microsoft.com/ServiceModel/Relay/`。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="d9c6d-153">hello 命名空間值不同於您在整個 hello 程式碼範圍內使用的 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="d9c6d-154">hello 命名空間值作為此合約，唯一的識別項，且必須有版本資訊。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="d9c6d-155">如需詳細資訊，請參閱[服務版本設定](http://go.microsoft.com/fwlink/?LinkID=180498)。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="d9c6d-156">明確指定 hello 命名空間，可防止 hello 預設命名空間值加入 toohello 合約名稱。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="d9c6d-157">Hello 內`IImageContract`介面，請宣告 hello 單一作業 hello 方法`IImageContract`hello 中的合約公開介面，並套用 hello`OperationContractAttribute`屬性為 hello 公開服務匯流排的一部分，想 tooexpose toohello 方法合約。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="d9c6d-158">在 hello **OperationContract**屬性，請將 hello **WebGet**值。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="d9c6d-159">這麼做會讓 hello 太 HTTP GET 要求的轉送服務 tooroute`GetImage`，並傳回值的 tootranslate hello`GetImage`成 HTTP GETRESPONSE 回覆。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="d9c6d-160">稍後在 hello 教學課程中，您將使用 web 瀏覽器 tooaccess 這個方法，以及 toodisplay hello 映像 hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="d9c6d-161">直接在 hello 之後`IImageContract`定義，宣告繼承自兩個 hello 通道`IImageContract`和`IClientChannel`介面。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="d9c6d-162">通道是 hello 服務與用戶端用來傳遞資訊 tooeach 其他 hello WCF 物件。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="d9c6d-163">稍後，您將建立 hello 通道在主控件應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="d9c6d-164">Azure 轉送然後會使用此通道 toopass hello HTTP GET 要求從 hello 瀏覽器 tooyour **GetImage**實作。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="d9c6d-165">hello 轉送也會使用 hello 通道 tootake hello **GetImage**傳回值，並將它轉譯成 HTTP GETRESPONSE hello 用戶端瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="d9c6d-166">從 hello**建置**功能表上，按一下 **建置方案**tooconfirm hello 精確度的工作為止。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="d9c6d-167">範例</span><span class="sxs-lookup"><span data-stu-id="d9c6d-167">Example</span></span>
<span data-ttu-id="d9c6d-168">下列程式碼的 hello 顯示定義的 WCF 轉送合約的基本介面。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="d9c6d-169">步驟 3： 實作 REST 式 WCF 服務合約 toouse 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="d9c6d-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="d9c6d-170">建立 rest 式 WCF 轉送服務，您必須先建立使用介面定義的 hello 合約。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="d9c6d-171">hello 下一個步驟是 tooimplement hello 介面。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="d9c6d-172">這項作業包括建立類別，名為**ImageService**實作使用者定義的 hello **IImageContract**介面。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="d9c6d-173">實作 hello 合約之後，接著您設定 hello 介面使用 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="d9c6d-174">hello 設定檔包含 hello 應用程式，例如 hello hello 服務名稱、 hello 名稱 hello 合約和通訊協定都使用的 toocommunicate 與 hello 轉送服務的 hello 類型的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="d9c6d-175">hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="d9c6d-176">因為與 hello 先前步驟中，沒有實作 rest 式合約與 WCF 轉送合約的差異很小。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="d9c6d-177">tooimplement rest 式服務匯流排合約</span><span class="sxs-lookup"><span data-stu-id="d9c6d-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="d9c6d-178">建立新的類別，名為**ImageService**的 hello 的 hello 定義之後，直接**IImageContract**介面。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="d9c6d-179">hello **ImageService**類別會實作 hello **IImageContract**介面。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="d9c6d-180">類似 tooother 介面實作，您可以實作 hello 定義不同的檔案中。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="d9c6d-181">不過，本教學課程，hello 實作會出現在相同檔案儲存為 hello 介面定義的 hello 和`Main()`方法。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="d9c6d-182">套用 hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx)屬性 toohello **IImageService** hello 類別的類別 tooindicate 是 WCF 合約的實作。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="d9c6d-183">如先前所述，此命名空間不是傳統的命名空間。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="d9c6d-184">相反地，它是 hello 識別 hello 合約的 WCF 架構的一部分。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="d9c6d-185">如需詳細資訊，請參閱 hello[資料合約名稱](https://msdn.microsoft.com/library/ms731045.aspx)hello WCF 文件中的主題。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="d9c6d-186">將.jpg 影像 tooyour 專案中。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="d9c6d-187">這是一個 hello 服務 hello 接收瀏覽器中顯示的圖片。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="d9c6d-188">以滑鼠右鍵按一下您的專案，然後按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="d9c6d-189">然後按一下 [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-189">Then click **Existing Item**.</span></span> <span data-ttu-id="d9c6d-190">使用 hello**加入現有項目**對話方塊方塊 toobrowse tooan 和適當的.jpg，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="d9c6d-191">加入時 hello 檔案，請確定**所有檔案**toohello 下一步的 hello 下拉式清單中選取**檔案名稱：**欄位。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="d9c6d-192">本教學課程的 hello rest 會假設該 hello hello 映像的名稱為"image.jpg"。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="d9c6d-193">如果您有不同的檔案，您將會有 toorename hello 映像，或變更程式碼 toocompensate。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="d9c6d-194">確定執行服務的 hello 可以尋找 hello 映像檔，在 toomake**方案總管] 中**hello 映像檔，以滑鼠右鍵按一下，然後按一下 [**屬性**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="d9c6d-195">在 [hello**屬性**] 窗格中，設定**複製 tooOutput 目錄**太**更新時才複製**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="d9c6d-196">新增參考 toohello **System.Drawing.dll** toohello 組件專案，以及將相關聯的 hello 下列`using`陳述式。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="d9c6d-197">在 hello **ImageService**類別中，加入 hello 下列建構函式載入 hello 點陣圖，並準備 toosend 它 toohello 用戶端瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
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
7. <span data-ttu-id="d9c6d-198">直接在 hello 先前的程式碼之後, 將 hello 面一行加入**GetImage**方法在 hello **ImageService**類別 tooreturn HTTP 訊息包含 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
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
   
    <span data-ttu-id="d9c6d-199">此實作會使用**MemoryStream** tooretrieve hello 映像，並準備進行串流處理 toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="d9c6d-200">它會啟動 hello 資料流位置在零處，宣告為 jpeg，hello 串流處理內容及資料流的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="d9c6d-201">從 hello**建置**功能表上，按一下 **建置方案**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="d9c6d-202">toodefine hello 設定服務匯流排上執行 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="d9c6d-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="d9c6d-203">在**方案總管 中**，連按兩下**App.config** tooopen hello Visual Studio 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="d9c6d-204">hello **App.config**檔案包含 hello 服務名稱、 端點 （也就是 hello 位置 Azure 轉送會公開為用戶端和主機彼此 toocommunicate），以及繫結 （通訊協定都使用的 toocommunicate hello 類型）。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="d9c6d-205">hello 主要的差異在於該 hello 設定服務端點會參考 tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding)繫結。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="d9c6d-206">hello `<system.serviceModel>` XML 項目會定義一個或多個服務的 WCF 項目。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="d9c6d-207">這裡是使用的 toodefine hello 服務名稱和端點。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="d9c6d-208">在 hello 底部 hello`<system.serviceModel>`項目 (但仍在`<system.serviceModel>`)，新增`<bindings>`hello 內容之後的項目。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="d9c6d-209">這會定義 hello hello 應用程式中使用的繫結。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="d9c6d-210">您可以定義多個繫結，但在本教學課程中您只會定義一個。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="d9c6d-211">hello 先前的程式碼定義的 WCF 轉送[WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding)繫結**relayClientAuthenticationType**設定得**無**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="d9c6d-212">這個設定表示使用此繫結的端點不需要用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="d9c6d-213">之後 hello`<bindings>`項目，加入`<services>`項目。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="d9c6d-214">類似 toohello 繫結，您可以在單一設定檔中定義多個服務。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="d9c6d-215">不過，您在本教學課程中只會定義一個。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="d9c6d-216">此步驟會設定使用預先定義的 hello 預設的服務**webHttpRelayBinding**。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="d9c6d-217">它也會使用預設 hello **sbTokenProvider**，定義在 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="d9c6d-218">之後 hello`<services>`項目，建立`<behaviors>`元素與 hello 內容之後，「 SAS_KEY"取代成 hello*共用存取簽章*(SAS) 金鑰，您先前取得的 hello [Azure 入口網站][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d9c6d-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="d9c6d-219">仍在 App.config 中，在 hello`<appSettings>`項目，使用您先前取得的 hello 入口網站的 hello 連接字串取代 hello 整個連接字串值。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="d9c6d-220">從 hello**建置**功能表上，按一下 **建置方案**toobuild hello 整個方案。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="d9c6d-221">範例</span><span class="sxs-lookup"><span data-stu-id="d9c6d-221">Example</span></span>
<span data-ttu-id="d9c6d-222">hello 下列程式碼顯示 hello 合約和服務實作，以 REST 為基礎的服務上執行的服務匯流排使用 hello **WebHttpRelayBinding**繫結。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="d9c6d-223">hello 下列範例顯示 hello 與 hello 服務相關聯的 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-223">hello following example shows hello App.config file associated with hello service.</span></span>

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

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="d9c6d-224">步驟 4： 主機 hello REST 式 WCF 服務 toouse Azure 轉送</span><span class="sxs-lookup"><span data-stu-id="d9c6d-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="d9c6d-225">此步驟說明如何 toorun web 服務的主控台應用程式使用 WCF 轉送。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="d9c6d-226">Hello 範例 hello 程序中提供 hello 撰寫的程式碼在此步驟中的完整清單。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="d9c6d-227">toocreate hello 服務的基底位址</span><span class="sxs-lookup"><span data-stu-id="d9c6d-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="d9c6d-228">在 hello`Main()`函式宣告中，建立變數 toostore hello 命名空間，您的專案。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="d9c6d-229">請確定 tooreplace `yourNamespace` hello hello 您先前建立的轉送命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="d9c6d-230">服務匯流排會使用您的唯一 URI 的命名空間 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="d9c6d-231">建立`Uri`hello 基底地址的 hello 命名空間為基礎的 hello 服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="d9c6d-232">toocreate 及設定 hello web 服務主機</span><span class="sxs-lookup"><span data-stu-id="d9c6d-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="d9c6d-233">建立 hello web 服務主機，請使用本節稍早建立的 hello URI 位址。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="d9c6d-234">hello 具現化 hello 主應用程式的 WCF 物件 hello 服務主機。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="d9c6d-235">此範例會將它 hello 類型要 toocreate 的主機 ( **ImageService**)，並也 hello 想 tooexpose hello 主應用程式的位址。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="d9c6d-236">toorun hello web 服務主機</span><span class="sxs-lookup"><span data-stu-id="d9c6d-236">toorun hello web service host</span></span>
1. <span data-ttu-id="d9c6d-237">開啟 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="d9c6d-238">hello 服務現在正在執行。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-238">hello service is now running.</span></span>
2. <span data-ttu-id="d9c6d-239">顯示訊息指示 hello 服務正在執行，且 toostop hello 服務的方式。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="d9c6d-240">完成後，關閉 hello 服務主機。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="d9c6d-241">範例</span><span class="sxs-lookup"><span data-stu-id="d9c6d-241">Example</span></span>
<span data-ttu-id="d9c6d-242">hello 下列範例包含主控台應用程式中的 hello 教學課程和主機 hello 服務中的 hello 服務合約和實作，從上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="d9c6d-243">編譯 hello 遵循成名為 ImageListener.exe 的可執行檔的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

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

### <a name="compiling-hello-code"></a><span data-ttu-id="d9c6d-244">編譯 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="d9c6d-244">Compiling hello code</span></span>
<span data-ttu-id="d9c6d-245">在建置之後 hello 方案，下列 toorun hello 應用程式 hello:</span><span class="sxs-lookup"><span data-stu-id="d9c6d-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="d9c6d-246">按**F5**，或瀏覽 toohello 可執行檔的位置 (ImageListener\bin\Debug\ImageListener.exe)，toorun hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="d9c6d-247">保持 hello 應用程式執行，它需要 tooperform hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="d9c6d-248">複製並貼到瀏覽器 toosee hello 映像的 hello 命令提示字元中的 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="d9c6d-249">當您完成時，請按**Enter** hello 命令提示字元 視窗 tooclose hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d9c6d-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9c6d-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9c6d-250">Next steps</span></span>
<span data-ttu-id="d9c6d-251">既然您已經建置使用 hello Service Bus 轉送服務的應用程式，請參閱下列文章 toolearn 更多關於 Azure 轉送 hello:</span><span class="sxs-lookup"><span data-stu-id="d9c6d-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="d9c6d-252">Azure 服務匯流排架構概觀</span><span class="sxs-lookup"><span data-stu-id="d9c6d-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="d9c6d-253">Azure 轉送概觀</span><span class="sxs-lookup"><span data-stu-id="d9c6d-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="d9c6d-254">如何 toouse hello WCF 轉送服務的.NET</span><span class="sxs-lookup"><span data-stu-id="d9c6d-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
