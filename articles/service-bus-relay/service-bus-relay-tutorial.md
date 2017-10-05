---
title: "Azure 服務匯流排 WCF 轉送教學課程 | Microsoft Docs"
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
ms.openlocfilehash: 5347bf85cad32b59677369d51a1f36529aef6662
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="2b99e-103">Azure WCF 轉送教學課程</span><span class="sxs-lookup"><span data-stu-id="2b99e-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="2b99e-104">本教學課程說明如何使用 Azure 轉送，來建置簡單的 WCF 轉送用戶端應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="2b99e-105">如需使用[服務匯流排通訊](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)的類似教學課程，請參閱[開始使用服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="2b99e-106">循序完成本教學課程，可讓您了解建立 WCF 轉送用戶端和服務應用程式所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="2b99e-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="2b99e-107">如同他們原始的 WCF 對應項目，服務是可公開一或多個端點的結構，而每個端點都會公開一或多個服務作業。</span><span class="sxs-lookup"><span data-stu-id="2b99e-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="2b99e-108">服務的端點指定可找到服務的位址、內含用戶端與服務通訊所需資訊的繫結，以及可定義服務提供給其用戶端之功能的合約。</span><span class="sxs-lookup"><span data-stu-id="2b99e-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="2b99e-109">WCF 與 WCF 轉送的主要差異在於端點是在雲端公開，而不是在您的電腦本機上公開。</span><span class="sxs-lookup"><span data-stu-id="2b99e-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="2b99e-110">在您逐步完成本教學課程中的各個主題後，您會有一項執行中的服務，以及可叫用服務作業的用戶端。</span><span class="sxs-lookup"><span data-stu-id="2b99e-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="2b99e-111">第一個主題說明如何設定帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b99e-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="2b99e-112">後續步驟說明如何定義使用合約的服務、如何實作服務，以及如何在程式碼中設定服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="2b99e-113">此外，也會說明如何主控和執行服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="2b99e-114">建立的服務會自我裝載，而用戶端和服務會在相同的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="2b99e-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="2b99e-115">您可以使用程式碼或組態檔來設定服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="2b99e-116">最後三個步驟描述如何建立用戶端應用程式、設定用戶端應用程式，以及建立和使用可存取主機功能的用戶端。</span><span class="sxs-lookup"><span data-stu-id="2b99e-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b99e-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="2b99e-117">Prerequisites</span></span>

<span data-ttu-id="2b99e-118">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="2b99e-118">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="2b99e-119">[Microsoft Visual Studio 2015 或更高版本](http://visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="2b99e-120">本教學課程使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="2b99e-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="2b99e-121">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b99e-121">An active Azure account.</span></span> <span data-ttu-id="2b99e-122">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b99e-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="2b99e-123">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="2b99e-124">建立服務命名空間</span><span class="sxs-lookup"><span data-stu-id="2b99e-124">Create a service namespace</span></span>

<span data-ttu-id="2b99e-125">第一個步驟是建立命名空間，並取得[共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b99e-125">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="2b99e-126">命名空間會為每個透過轉送服務公開的應用程式提供應用程式界限。</span><span class="sxs-lookup"><span data-stu-id="2b99e-126">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="2b99e-127">建立服務命名空間時，系統會自動產生 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b99e-127">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="2b99e-128">服務命名空間與 SAS 金鑰的組合會提供一個認證，供 Azure 用來驗證對應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="2b99e-128">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="2b99e-129">請依照[這裡的指示](relay-create-namespace-portal.md)來建立轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="2b99e-129">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="2b99e-130">定義 WCF 服務合約</span><span class="sxs-lookup"><span data-stu-id="2b99e-130">Define a WCF service contract</span></span>

<span data-ttu-id="2b99e-131">服務合約會指定服務可支援哪些作業 (方法或函式的 Web 服務術語)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-131">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="2b99e-132">合約可以透過定義 C++、C# 或 Visual Basic 介面建立。</span><span class="sxs-lookup"><span data-stu-id="2b99e-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="2b99e-133">介面中的每個方法會對應一個特定服務作業。</span><span class="sxs-lookup"><span data-stu-id="2b99e-133">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="2b99e-134">每個介面都必須已套用 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 屬性，而且每個作業都必須已套用 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 屬性。</span><span class="sxs-lookup"><span data-stu-id="2b99e-134">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="2b99e-135">如果介面中的方法有 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 屬性，但沒有 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 屬性，則不會公開該方法。</span><span class="sxs-lookup"><span data-stu-id="2b99e-135">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="2b99e-136">程序後面的範例會提供這些工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b99e-136">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="2b99e-137">如需合約與服務的詳細討論，請參閱 WCF 文件中的[設計和實作服務](https://msdn.microsoft.com/library/ms729746.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="2b99e-138">使用介面建立轉送合約</span><span class="sxs-lookup"><span data-stu-id="2b99e-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="2b99e-139">以系統管理員身分開啟 Visual Studio：以滑鼠右鍵按一下 [開始] 功能表中的程式，然後選取 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-139">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="2b99e-140">這會建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-140">Create a new console application project.</span></span> <span data-ttu-id="2b99e-141">按一下 [檔案] 功能表，選取 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-141">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="2b99e-142">在 [新增專案] 對話方塊中，按一下 **Visual C#** (如果 **Visual C#** 未出現，請查看 [其他語言] 下方)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-142">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="2b99e-143">按一下 [主控台應用程式 (.NET Framework)] 範本，並將它命名為 **EchoService**。</span><span class="sxs-lookup"><span data-stu-id="2b99e-143">Click the **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="2b99e-144">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-144">Click **OK** to create the project.</span></span>

    ![][2]

3. <span data-ttu-id="2b99e-145">安裝服務匯流排 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="2b99e-145">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="2b99e-146">此套件會自動新增服務匯流排程式庫及 WCF **System.ServiceModel** 的參考。</span><span class="sxs-lookup"><span data-stu-id="2b99e-146">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="2b99e-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) 是可讓您以程式設計方式存取 WCF 基本功能的命名空間。</span><span class="sxs-lookup"><span data-stu-id="2b99e-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="2b99e-148">服務匯流排會使用 WCF 的許多物件和屬性來定義服務合約。</span><span class="sxs-lookup"><span data-stu-id="2b99e-148">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="2b99e-149">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-149">In Solution Explorer, right-click the project, and then click **Manage NuGet Packages...**.</span></span> <span data-ttu-id="2b99e-150">按一下 [瀏覽] 索引標籤，然後搜尋 `Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="2b99e-150">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="2b99e-151">確定已在 [版本] 方塊中選取此專案名稱。</span><span class="sxs-lookup"><span data-stu-id="2b99e-151">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="2b99e-152">按一下 [安裝] 並接受使用條款。</span><span class="sxs-lookup"><span data-stu-id="2b99e-152">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="2b99e-153">在 [方案總管] 中，按兩下 Program.cs 檔案，以在編輯器中開啟它 (如果尚未開啟的話)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-153">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="2b99e-154">在檔案頂端加入下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="2b99e-154">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="2b99e-155">將命名空間名稱從 **EchoService** 的預設名稱變更為 **Microsoft.ServiceBus.Samples**。</span><span class="sxs-lookup"><span data-stu-id="2b99e-155">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2b99e-156">本教學課程使用 C# 命名空間 **Microsoft.ServiceBus.Samples**，也就是在[設定 WCF 用戶端](#configure-the-wcf-client)步驟的設定檔中所使用合約型 Managed 型別的命名空間。</span><span class="sxs-lookup"><span data-stu-id="2b99e-156">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract-based managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="2b99e-157">您可以在建置此範例時指定您要的任何命名空間；不過，除非您後來在應用程式組態檔中相應地修改合約的命名空和服務，否則本教學課程將無法運作。</span><span class="sxs-lookup"><span data-stu-id="2b99e-157">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="2b99e-158">在 App.config 檔案中指定的命名空間必須與在 C# 檔案中指定的命名空間相同。</span><span class="sxs-lookup"><span data-stu-id="2b99e-158">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="2b99e-159">緊接在 `Microsoft.ServiceBus.Samples` 命名空間宣告後面 (但在命名空間內)，定義名為 `IEchoContract` 的新介面，並將 `ServiceContractAttribute` 屬性套用至命名空間值為 `http://samples.microsoft.com/ServiceModel/Relay/` 的介面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-159">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="2b99e-160">命名空間值與您的整個程式碼範圍中使用的命名空間不同。</span><span class="sxs-lookup"><span data-stu-id="2b99e-160">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="2b99e-161">然而，命名空間值會作為此合約的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="2b99e-161">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="2b99e-162">明確指定命名空間可避免將預設命名空間值新增至合約名稱。</span><span class="sxs-lookup"><span data-stu-id="2b99e-162">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span> <span data-ttu-id="2b99e-163">將下列程式碼貼上到命名空間宣告之後：</span><span class="sxs-lookup"><span data-stu-id="2b99e-163">Paste the following code after the namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="2b99e-164">一般而言，服務合約命名空間包含命名配置 (其中包含版本資訊)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-164">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="2b99e-165">在服務合約命名空間中包含版本資訊，可讓服務定義具有新命名空間的新服務合約並在新的端點上公開它，藉此區隔重大變更。</span><span class="sxs-lookup"><span data-stu-id="2b99e-165">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="2b99e-166">如此一來，用戶端可以繼續使用舊服務合約，而不需要更新。</span><span class="sxs-lookup"><span data-stu-id="2b99e-166">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="2b99e-167">版本資訊可以包含日期或組建編號。</span><span class="sxs-lookup"><span data-stu-id="2b99e-167">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="2b99e-168">如需詳細資訊，請參閱[服務版本設定](http://go.microsoft.com/fwlink/?LinkID=180498)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-168">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="2b99e-169">基於本教學課程的目的，服務合約命名空間的命名配置不包含版本資訊。</span><span class="sxs-lookup"><span data-stu-id="2b99e-169">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="2b99e-170">在 `IEchoContract` 介面中，針對 `IEchoContract` 合約在介面中公開的單一作業宣告方法，並將 `OperationContractAttribute` 屬性套用至您想要公開為公用 WCF 轉送合約一部分的方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b99e-170">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="2b99e-171">直接在 `IEchoContract` 介面定義之後，宣告同時繼承自 `IEchoContract` 與 `IClientChannel` 介面的通道，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b99e-171">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="2b99e-172">通道是 WCF 物件，主機和用戶端可透過它彼此傳遞資訊。</span><span class="sxs-lookup"><span data-stu-id="2b99e-172">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="2b99e-173">稍後，您將對此通道撰寫程式碼，以回應兩個應用程式之間的資訊。</span><span class="sxs-lookup"><span data-stu-id="2b99e-173">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="2b99e-174">從 [建置] 功能表中，按一下 [建置方案] 或按 **Ctrl+Shift+B**，確認到目前為止您的工作正確無誤。</span><span class="sxs-lookup"><span data-stu-id="2b99e-174">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="2b99e-175">範例</span><span class="sxs-lookup"><span data-stu-id="2b99e-175">Example</span></span>

<span data-ttu-id="2b99e-176">下列程式碼示範定義 WCF 轉送合約的基本介面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-176">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="2b99e-177">現在已建立介面，您可以實作此介面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-177">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="2b99e-178">實作 WCF 合約</span><span class="sxs-lookup"><span data-stu-id="2b99e-178">Implement the WCF contract</span></span>

<span data-ttu-id="2b99e-179">建立 Azure 轉送需要先建立合約，您可使用介面定義該合約。</span><span class="sxs-lookup"><span data-stu-id="2b99e-179">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="2b99e-180">如需建立介面的詳細資訊，請參閱上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="2b99e-180">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="2b99e-181">下一步是實作介面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-181">The next step is to implement the interface.</span></span> <span data-ttu-id="2b99e-182">這牽涉到建立名為 `EchoService` 的類別，該類別會實作使用者定義的 `IEchoContract` 介面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-182">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="2b99e-183">實作合約後，接著可使用 App.config 組態檔設定介面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-183">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="2b99e-184">組態檔包含應用程式的必要資訊，例如服務名稱、合約名稱，以及用來與轉送服務通訊的通訊協定類型。</span><span class="sxs-lookup"><span data-stu-id="2b99e-184">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="2b99e-185">程序後面的範例提供用來執行這些工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b99e-185">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="2b99e-186">如需如何實作服務合約的一般討論，請參閱 WCF 文件中的[實作服務合約](https://msdn.microsoft.com/library/ms733764.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-186">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="2b99e-187">緊接在 `IEchoContract` 介面的定義之後，建立名為 `EchoService` 的新類別。</span><span class="sxs-lookup"><span data-stu-id="2b99e-187">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="2b99e-188">`EchoService` 類別會實作 `IEchoContract` 介面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-188">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="2b99e-189">類似於其他介面實作，您可以在不同的檔案中實作定義。</span><span class="sxs-lookup"><span data-stu-id="2b99e-189">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="2b99e-190">不過，在此教學課程中，實作會位於與介面定義和 `Main` 方法相同的檔案中。</span><span class="sxs-lookup"><span data-stu-id="2b99e-190">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="2b99e-191">將 [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) 屬性套用至 `IEchoContract` 介面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-191">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="2b99e-192">此屬性會指定服務名稱和命名空間。</span><span class="sxs-lookup"><span data-stu-id="2b99e-192">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="2b99e-193">這麼做之後，`EchoService` 類別會如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2b99e-193">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="2b99e-194">實作在 `EchoService` 類別的 `IEchoContract` 介面中定義的 `Echo` 方法。</span><span class="sxs-lookup"><span data-stu-id="2b99e-194">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="2b99e-195">按一下 [建置]，然後按一下 [建置方案]，確認您的工作正確無誤。</span><span class="sxs-lookup"><span data-stu-id="2b99e-195">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="define-the-configuration-for-the-service-host"></a><span data-ttu-id="2b99e-196">定義服務主機的設定</span><span class="sxs-lookup"><span data-stu-id="2b99e-196">Define the configuration for the service host</span></span>

1. <span data-ttu-id="2b99e-197">此組態檔非常類似於 WCF 組態檔。</span><span class="sxs-lookup"><span data-stu-id="2b99e-197">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="2b99e-198">其中包含服務名稱、端點 (也就是 Azure 轉送公開的位置，讓用戶端與主機能夠彼此通訊) 和繫結 (用於通訊的通訊協定類型)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-198">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="2b99e-199">主要差異在於這個已設定的服務端點會參考不屬於 .NET Framework 的 [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) 繫結。</span><span class="sxs-lookup"><span data-stu-id="2b99e-199">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="2b99e-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) 是服務所定義的其中一個繫結。</span><span class="sxs-lookup"><span data-stu-id="2b99e-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="2b99e-201">在 [方案總管] 中，按兩下 App.config 檔案，以在 Visual Studio 編輯器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="2b99e-201">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="2b99e-202">在 `<appSettings>` 元素中，以您的服務命名空間名稱以及您在先前步驟中複製的 SAS 金鑰取代預留位置。</span><span class="sxs-lookup"><span data-stu-id="2b99e-202">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="2b99e-203">在 `<system.serviceModel>` 標記內，加入 `<services>` 元素。</span><span class="sxs-lookup"><span data-stu-id="2b99e-203">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="2b99e-204">您可以在單一組態檔中定義多個轉送應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b99e-204">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="2b99e-205">不過，本教學課程只會定義一個。</span><span class="sxs-lookup"><span data-stu-id="2b99e-205">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="2b99e-206">在 `<services>` 元素內，加入 `<service>` 元素以定義服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="2b99e-206">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="2b99e-207">在 `<service>` 元素內，定義端點合約的位置，以及端點的繫結類型。</span><span class="sxs-lookup"><span data-stu-id="2b99e-207">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="2b99e-208">端點會定義用戶端將在何處尋找主應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b99e-208">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="2b99e-209">稍後，本教學課程會使用此步驟來建立 URI，以透過 Azure 轉送完全公開主機。</span><span class="sxs-lookup"><span data-stu-id="2b99e-209">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="2b99e-210">繫結會宣告我們使用 TCP 作為與轉送服務通訊的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2b99e-210">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="2b99e-211">從 [建置] 功能表中，按一下 [建置方案]，確認您的工作正確無誤。</span><span class="sxs-lookup"><span data-stu-id="2b99e-211">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="2b99e-212">範例</span><span class="sxs-lookup"><span data-stu-id="2b99e-212">Example</span></span>

<span data-ttu-id="2b99e-213">下列程式碼示範服務合約的實作。</span><span class="sxs-lookup"><span data-stu-id="2b99e-213">The following code shows the implementation of the service contract.</span></span>

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

<span data-ttu-id="2b99e-214">下列程式碼顯示與服務相關聯之 App.config 檔案的基本格式。</span><span class="sxs-lookup"><span data-stu-id="2b99e-214">The following code shows the basic format of the App.config file associated with the service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="2b99e-215">裝載並執行基本 Web 服務以向轉送服務登錄</span><span class="sxs-lookup"><span data-stu-id="2b99e-215">Host and run a basic web service to register with the relay service</span></span>

<span data-ttu-id="2b99e-216">此步驟描述如何執行 Azure 轉送服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-216">This step describes how to run an Azure Relay service.</span></span>

### <a name="create-the-relay-credentials"></a><span data-ttu-id="2b99e-217">建立轉送認證</span><span class="sxs-lookup"><span data-stu-id="2b99e-217">Create the relay credentials</span></span>

1. <span data-ttu-id="2b99e-218">在 `Main()` 中，建立兩個變數，以儲存命名空間以及從主控台視窗讀取的 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b99e-218">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="2b99e-219">SAS 金鑰稍後將用來存取您的專案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-219">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="2b99e-220">命名空間會當做參數傳遞至 `CreateServiceUri` 以建立服務 URI。</span><span class="sxs-lookup"><span data-stu-id="2b99e-220">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="2b99e-221">使用 [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) 物件，宣告您將使用 SAS 金鑰作為認證類型。</span><span class="sxs-lookup"><span data-stu-id="2b99e-221">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="2b99e-222">將下列程式碼直接加在最後一個步驟中新增的程式碼之後。</span><span class="sxs-lookup"><span data-stu-id="2b99e-222">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a><span data-ttu-id="2b99e-223">建立服務的基底位址</span><span class="sxs-lookup"><span data-stu-id="2b99e-223">Create a base address for the service</span></span>

<span data-ttu-id="2b99e-224">在最後一個步驟中加入的程式碼後面，建立服務基底位址的 `Uri` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="2b99e-224">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="2b99e-225">此 URI 會指定服務匯流排配置、命名空間和服務介面的路徑。</span><span class="sxs-lookup"><span data-stu-id="2b99e-225">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="2b99e-226">"sb" 是服務匯流排配置的縮寫，並指出我們使用 TCP 作為通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2b99e-226">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="2b99e-227">當 [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) 被指定為繫結時，先前也已在組態檔中指出此項。</span><span class="sxs-lookup"><span data-stu-id="2b99e-227">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="2b99e-228">在本教學課程中，URI 為 `sb://putServiceNamespaceHere.windows.net/EchoService`。</span><span class="sxs-lookup"><span data-stu-id="2b99e-228">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-the-service-host"></a><span data-ttu-id="2b99e-229">建立並設定服務主機</span><span class="sxs-lookup"><span data-stu-id="2b99e-229">Create and configure the service host</span></span>

1. <span data-ttu-id="2b99e-230">將連線模式設定為 `AutoDetect`。</span><span class="sxs-lookup"><span data-stu-id="2b99e-230">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="2b99e-231">連線模式可描述服務用來與轉送服務通訊的通訊協定 (HTTP 或 TCP)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-231">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="2b99e-232">使用預設設定 `AutoDetect`，服務會嘗試透過 TCP 連接至 Azure 轉送，如果無法使用 TCP，則會透過 HTTP 連接。</span><span class="sxs-lookup"><span data-stu-id="2b99e-232">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="2b99e-233">請注意，這有別於服務針對用戶端通訊指定的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2b99e-233">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="2b99e-234">該通訊協定取決於使用的繫結。</span><span class="sxs-lookup"><span data-stu-id="2b99e-234">That protocol is determined by the binding used.</span></span> <span data-ttu-id="2b99e-235">例如，服務可以使用 [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) 繫結，指定它的端點會透過 HTTP 來與用戶端通訊。</span><span class="sxs-lookup"><span data-stu-id="2b99e-235">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="2b99e-236">該相同服務可以指定 **ConnectivityMode.AutoDetect**，讓服務能夠透過 TCP 來與 Azure 轉送通訊。</span><span class="sxs-lookup"><span data-stu-id="2b99e-236">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="2b99e-237">使用本節稍早建立的 URI，建立服務主機。</span><span class="sxs-lookup"><span data-stu-id="2b99e-237">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="2b99e-238">服務主機是將服務具現化的 WCF 物件。</span><span class="sxs-lookup"><span data-stu-id="2b99e-238">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="2b99e-239">在此，您會將您要建立的服務類型 (`EchoService` 類型)，以及您要公開服務的位址傳給它。</span><span class="sxs-lookup"><span data-stu-id="2b99e-239">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="2b99e-240">在 Program.cs 檔案頂端，加入 [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) 和 [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description) 的參考。</span><span class="sxs-lookup"><span data-stu-id="2b99e-240">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="2b99e-241">回到 `Main()`，設定要啟用公開存取的端點。</span><span class="sxs-lookup"><span data-stu-id="2b99e-241">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="2b99e-242">此步驟會通知轉送服務，藉由檢查專案的 ATOM 摘要，公開找到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b99e-242">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="2b99e-243">如果您將 **DiscoveryType** 設定為 [私人]，用戶端仍可存取服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-243">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="2b99e-244">不過，服務在搜尋轉送命名空間時並不會出現。</span><span class="sxs-lookup"><span data-stu-id="2b99e-244">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="2b99e-245">相反地，用戶端必須事先知道端點路徑。</span><span class="sxs-lookup"><span data-stu-id="2b99e-245">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="2b99e-246">將服務認證套用至在 App.config 檔案中定義的服務端點︰</span><span class="sxs-lookup"><span data-stu-id="2b99e-246">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="2b99e-247">如上一個步驟所述，您可能已在組態檔中宣告多個服務和端點。</span><span class="sxs-lookup"><span data-stu-id="2b99e-247">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="2b99e-248">若是如此，此程式碼會周遊組態檔及搜尋每個應套用您的認證的端點。</span><span class="sxs-lookup"><span data-stu-id="2b99e-248">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="2b99e-249">不過，在本教學課程中，組態檔只有一個端點。</span><span class="sxs-lookup"><span data-stu-id="2b99e-249">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="open-the-service-host"></a><span data-ttu-id="2b99e-250">開啟服務主機</span><span class="sxs-lookup"><span data-stu-id="2b99e-250">Open the service host</span></span>

1. <span data-ttu-id="2b99e-251">開啟服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-251">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="2b99e-252">通知使用者此服務正在執行，以及說明如何關閉服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-252">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="2b99e-253">完成時，關閉服務主機。</span><span class="sxs-lookup"><span data-stu-id="2b99e-253">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="2b99e-254">按 **Ctrl+Shift+B** 建置專案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-254">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="2b99e-255">範例</span><span class="sxs-lookup"><span data-stu-id="2b99e-255">Example</span></span>

<span data-ttu-id="2b99e-256">完整的服務程式碼應如下所示。</span><span class="sxs-lookup"><span data-stu-id="2b99e-256">Your completed service code should appear as follows.</span></span> <span data-ttu-id="2b99e-257">程式碼包括教學課程先前步驟的服務合約和實作，並在主控台應用程式中裝載服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-257">The code includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span>

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

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="2b99e-258">建立服務合約的 WCF 用戶端</span><span class="sxs-lookup"><span data-stu-id="2b99e-258">Create a WCF client for the service contract</span></span>

<span data-ttu-id="2b99e-259">下一個步驟是建立用戶端應用程式，並定義您將在後續步驟中實作的服務合約。</span><span class="sxs-lookup"><span data-stu-id="2b99e-259">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="2b99e-260">請注意，這其中有許多步驟類似於用來建立服務的步驟︰定義合約、編輯 App.config 檔案、使用認證來連接至轉送服務等等。</span><span class="sxs-lookup"><span data-stu-id="2b99e-260">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="2b99e-261">程序後面的範例提供用來執行這些工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b99e-261">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="2b99e-262">若要在目前的 Visual Studio 方案中為用戶端建立新專案，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="2b99e-262">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="2b99e-263">在方案總管中含有服務的相同方案中，以滑鼠右鍵按一下目前的方案 (而非專案)，然後按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-263">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="2b99e-264">然後按一下 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-264">Then click **New Project**.</span></span>
   2. <span data-ttu-id="2b99e-265">在 [新增專案] 對話方塊中，按一下 [Visual C#] \(如果 **Visual C#** 未出現，請在 [其他語言] 下尋找)，選取 [主控台應用程式 (.NET Framework)] 範本，並將它命名為 **EchoClient**。</span><span class="sxs-lookup"><span data-stu-id="2b99e-265">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="2b99e-266">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-266">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="2b99e-267">在 [方案總管] 中，按兩下 **EchoClient** 專案中的 Program.cs 檔案，以在編輯器中開啟它 (如果尚未開啟的話)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-267">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="2b99e-268">將命名空間名稱從 `EchoClient` 的預設名稱變更為 `Microsoft.ServiceBus.Samples`。</span><span class="sxs-lookup"><span data-stu-id="2b99e-268">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="2b99e-269">安裝[服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)：在 [方案總管] 中，以滑鼠右鍵按一下 **EchoClient** 專案，然後按一下 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-269">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="2b99e-270">按一下 [瀏覽] 索引標籤，然後搜尋 `Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="2b99e-270">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="2b99e-271">按一下 [安裝] 並接受使用條款。</span><span class="sxs-lookup"><span data-stu-id="2b99e-271">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="2b99e-272">在 Program.cs 檔案中加入 [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) 命名空間的 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="2b99e-272">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="2b99e-273">下列範例所示，將服務合約定義新增至命名空間。</span><span class="sxs-lookup"><span data-stu-id="2b99e-273">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="2b99e-274">請注意，此定義與 [服務] 專案中使用的定義相同。</span><span class="sxs-lookup"><span data-stu-id="2b99e-274">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="2b99e-275">您應該在 `Microsoft.ServiceBus.Samples` 命名空間的頂端加入此程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b99e-275">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="2b99e-276">按 **Ctrl+Shift+B** 建置用戶端。</span><span class="sxs-lookup"><span data-stu-id="2b99e-276">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="2b99e-277">範例</span><span class="sxs-lookup"><span data-stu-id="2b99e-277">Example</span></span>

<span data-ttu-id="2b99e-278">下列程式碼顯示 **EchoClient** 專案中 Program.cs 檔案的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="2b99e-278">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

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

## <a name="configure-the-wcf-client"></a><span data-ttu-id="2b99e-279">設定 WCF 用戶端</span><span class="sxs-lookup"><span data-stu-id="2b99e-279">Configure the WCF client</span></span>

<span data-ttu-id="2b99e-280">在此步驟中，您可為基本用戶端應用程式建立 App.config 檔案，以存取先前在本教學課程中建立的服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-280">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="2b99e-281">此 App.config 檔案定義端點的合約、繫結和名稱。</span><span class="sxs-lookup"><span data-stu-id="2b99e-281">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="2b99e-282">程序後面的範例提供用來執行這些工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b99e-282">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="2b99e-283">在 [方案總管] 的 **EchoClient** 專案中，按兩下 **App.config**，在 Visual Studio 編輯器中開啟該檔案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-283">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="2b99e-284">在 `<appSettings>` 元素中，以您的服務命名空間名稱以及您在先前步驟中複製的 SAS 金鑰取代預留位置。</span><span class="sxs-lookup"><span data-stu-id="2b99e-284">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="2b99e-285">在 system.serviceModel 元素中加入 `<client>` 元素。</span><span class="sxs-lookup"><span data-stu-id="2b99e-285">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="2b99e-286">此步驟宣告您正在定義 WCF 樣式的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b99e-286">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="2b99e-287">在 `client` 元素內，定義端點的名稱、合約和繫結類型。</span><span class="sxs-lookup"><span data-stu-id="2b99e-287">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="2b99e-288">此步驟會定義端點的名稱、服務中定義的合約，以及用戶端應用程式使用 TCP 來與 Azure 轉送通訊的細節。</span><span class="sxs-lookup"><span data-stu-id="2b99e-288">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="2b99e-289">端點名稱在下一步中用來連結此端點組態與服務 URI。</span><span class="sxs-lookup"><span data-stu-id="2b99e-289">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="2b99e-290">按一下 [檔案]，然後按一下 [全部儲存]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-290">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="2b99e-291">範例</span><span class="sxs-lookup"><span data-stu-id="2b99e-291">Example</span></span>

<span data-ttu-id="2b99e-292">下列程式碼會顯示 Echo 用戶端的 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-292">The following code shows the App.config file for the Echo client.</span></span>

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

## <a name="implement-the-wcf-client"></a><span data-ttu-id="2b99e-293">實作 WCF 用戶端</span><span class="sxs-lookup"><span data-stu-id="2b99e-293">Implement the WCF client</span></span>
<span data-ttu-id="2b99e-294">在此步驟中，您可實作基本用戶端應用程式，以存取您先前在本教學課程中建立的服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-294">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="2b99e-295">與此服務類似，用戶端會執行許多相同的作業來存取 Azure 轉送：</span><span class="sxs-lookup"><span data-stu-id="2b99e-295">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="2b99e-296">設定連線模式。</span><span class="sxs-lookup"><span data-stu-id="2b99e-296">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="2b99e-297">建立可找出主機服務的 URI。</span><span class="sxs-lookup"><span data-stu-id="2b99e-297">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="2b99e-298">定義安全性認證。</span><span class="sxs-lookup"><span data-stu-id="2b99e-298">Defines the security credentials.</span></span>
4. <span data-ttu-id="2b99e-299">將認證套用至連線。</span><span class="sxs-lookup"><span data-stu-id="2b99e-299">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="2b99e-300">開啟連線。</span><span class="sxs-lookup"><span data-stu-id="2b99e-300">Opens the connection.</span></span>
6. <span data-ttu-id="2b99e-301">執行應用程式特定的工作。</span><span class="sxs-lookup"><span data-stu-id="2b99e-301">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="2b99e-302">關閉連線。</span><span class="sxs-lookup"><span data-stu-id="2b99e-302">Closes the connection.</span></span>

<span data-ttu-id="2b99e-303">不過，其中一個主要差異在於用戶端應用程式會使用通道來連接至轉送服務，而此服務會使用對 **ServiceHost** 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="2b99e-303">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="2b99e-304">程序後面的範例提供用來執行這些工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b99e-304">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="2b99e-305">實作用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="2b99e-305">Implement a client application</span></span>
1. <span data-ttu-id="2b99e-306">將連線模式設定為 [自動偵測]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-306">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="2b99e-307">在 **EchoClient** 應用程式的 `Main()` 方法中新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b99e-307">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="2b99e-308">定義變數，以保留服務命名空間以及從主控台讀取之 SAS 金鑰的值。</span><span class="sxs-lookup"><span data-stu-id="2b99e-308">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="2b99e-309">建立可定義轉送專案中主機位置的 URI。</span><span class="sxs-lookup"><span data-stu-id="2b99e-309">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="2b99e-310">建立服務命名空間端點的認證物件。</span><span class="sxs-lookup"><span data-stu-id="2b99e-310">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="2b99e-311">建立通道工廠，以載入 App.config 檔案中所述的組態。</span><span class="sxs-lookup"><span data-stu-id="2b99e-311">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="2b99e-312">通道工廠是一個 WCF 物件，可建立通道以供服務與用戶端應用程式進行通訊。</span><span class="sxs-lookup"><span data-stu-id="2b99e-312">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="2b99e-313">套用認證。</span><span class="sxs-lookup"><span data-stu-id="2b99e-313">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="2b99e-314">建立並開啟服務的通道。</span><span class="sxs-lookup"><span data-stu-id="2b99e-314">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="2b99e-315">撰寫 Echo 的基本使用者介面和功能。</span><span class="sxs-lookup"><span data-stu-id="2b99e-315">Write the basic user interface and functionality for the echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

    <span data-ttu-id="2b99e-316">請注意，程式碼會使用通道物件的執行個體作為服務的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="2b99e-316">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="2b99e-317">關閉通道，並關閉工廠。</span><span class="sxs-lookup"><span data-stu-id="2b99e-317">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="2b99e-318">範例</span><span class="sxs-lookup"><span data-stu-id="2b99e-318">Example</span></span>

<span data-ttu-id="2b99e-319">完整的程式碼應如下所示，顯示如何建立用戶端應用程式、如何呼叫服務的作業，以及如何在完成作業呼叫之後關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="2b99e-319">Your completed code should appear as follows, showing how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

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

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

## <a name="run-the-applications"></a><span data-ttu-id="2b99e-320">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="2b99e-320">Run the applications</span></span>

1. <span data-ttu-id="2b99e-321">按 **Ctrl+Shift+B** 以建置方案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-321">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="2b99e-322">這會建置您在先前步驟中建立的用戶端專案和服務專案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-322">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="2b99e-323">執行用戶端應用程式之前，您必須確定服務應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="2b99e-323">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="2b99e-324">在 Visual Studio 的 [方案總管] 中，以滑鼠右鍵按一下 **EchoService** 方案，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-324">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="2b99e-325">在 [方案屬性] 對話方塊中，按一下 [啟始專案]，然後按一下 [多個啟始專案] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2b99e-325">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="2b99e-326">確定 **EchoService** 顯示在清單中的最前面。</span><span class="sxs-lookup"><span data-stu-id="2b99e-326">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="2b99e-327">將 **EchoService** 和 **EchoClient** 專案的 [動作] 方塊設定為 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-327">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="2b99e-328">按一下 [專案相依性]。</span><span class="sxs-lookup"><span data-stu-id="2b99e-328">Click **Project Dependencies**.</span></span> <span data-ttu-id="2b99e-329">在 [專案] 方塊中，選取 **EchoClient**。</span><span class="sxs-lookup"><span data-stu-id="2b99e-329">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="2b99e-330">在 [取決於] 方塊中，確定已核取 **EchoService**。</span><span class="sxs-lookup"><span data-stu-id="2b99e-330">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="2b99e-331">按一下 [確定] 以關閉 [屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2b99e-331">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="2b99e-332">按 **F5** 執行這兩個專案。</span><span class="sxs-lookup"><span data-stu-id="2b99e-332">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="2b99e-333">兩個主控台視窗隨即開啟並提示您輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="2b99e-333">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="2b99e-334">必須先執行服務，因此在 **EchoService** 主控台視窗中輸入命名空間，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="2b99e-334">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="2b99e-335">接下來，系統會提示您輸入 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b99e-335">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="2b99e-336">輸入 SAS 金鑰並按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="2b99e-336">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="2b99e-337">以下是主控台視窗的範例輸出。</span><span class="sxs-lookup"><span data-stu-id="2b99e-337">Here is example output from the console window.</span></span> <span data-ttu-id="2b99e-338">請注意，此處提供的值僅適用於範例。</span><span class="sxs-lookup"><span data-stu-id="2b99e-338">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="2b99e-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="2b99e-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="2b99e-340">服務應用程式會將它所接聽的位址列印到主控台視窗，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="2b99e-340">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="2b99e-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="2b99e-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="2b99e-342">在 **EchoClient** 主控台視窗中，輸入您先前針對此服務應用程式輸入的相同資訊。</span><span class="sxs-lookup"><span data-stu-id="2b99e-342">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="2b99e-343">遵循上述步驟，為此用戶端應用程式輸入相同的服務命名空間和 SAS 金鑰值。</span><span class="sxs-lookup"><span data-stu-id="2b99e-343">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="2b99e-344">輸入這些值後，用戶端就會開啟服務通道，並提示您輸入一些文字，如下列主控台輸出範例所示。</span><span class="sxs-lookup"><span data-stu-id="2b99e-344">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="2b99e-345">輸入一些文字以傳送至服務應用程式並按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="2b99e-345">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="2b99e-346">這段文字會透過 Echo 服務作業傳送至服務，並如下列範例輸出所示出現在服務主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="2b99e-346">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="2b99e-347">用戶端應用程式會接收 `Echo` 作業的傳回值 (此值是原始文字)，並將它列印至主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="2b99e-347">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="2b99e-348">以下是用戶端主控台視窗的範例輸出。</span><span class="sxs-lookup"><span data-stu-id="2b99e-348">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="2b99e-349">您可以繼續以這種方式將文字訊息從用戶端傳送至服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-349">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="2b99e-350">完成後，在用戶端和服務主控台視窗中按 Enter 鍵以結束這兩個應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b99e-350">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b99e-351">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b99e-351">Next steps</span></span>

<span data-ttu-id="2b99e-352">本教學課程示範了如何使用服務匯流排的 WCF 轉送功能，來建置 Azure 轉送用戶端應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="2b99e-352">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="2b99e-353">如需使用[服務匯流排通訊](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)的類似教學課程，請參閱[開始使用服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="2b99e-353">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="2b99e-354">若要深入了解 Azure 轉送，請參閱下列主題。</span><span class="sxs-lookup"><span data-stu-id="2b99e-354">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="2b99e-355">Azure 服務匯流排架構概觀</span><span class="sxs-lookup"><span data-stu-id="2b99e-355">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="2b99e-356">Azure 轉送概觀</span><span class="sxs-lookup"><span data-stu-id="2b99e-356">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="2b99e-357">如何使用 WCF 轉送服務搭配 .NET</span><span class="sxs-lookup"><span data-stu-id="2b99e-357">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
