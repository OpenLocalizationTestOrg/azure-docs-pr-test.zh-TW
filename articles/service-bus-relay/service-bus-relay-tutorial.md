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
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="d71fa-103">Azure WCF 轉送教學課程</span><span class="sxs-lookup"><span data-stu-id="d71fa-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="d71fa-104">本教學課程將告訴您如何 toobuild 簡單的 WCF 轉送用戶端應用程式和使用 Azure 轉送服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="d71fa-105">如需使用[服務匯流排通訊](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)的類似教學課程，請參閱[開始使用服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="d71fa-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="d71fa-106">在本教學課程的工作可讓您了解必要的 toocreate 的 WCF 轉送的用戶端和服務應用程式的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d71fa-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="d71fa-107">如同他們原始的 WCF 對應項目，服務是可公開一或多個端點的結構，而每個端點都會公開一或多個服務作業。</span><span class="sxs-lookup"><span data-stu-id="d71fa-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="d71fa-108">hello 的服務端點指定 hello 服務可以找到的位址的繫結，其中包含用戶端必須與 hello 服務，以及定義 hello 服務 tooits 用戶端所提供的 hello 功能的合約進行通訊的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="d71fa-109">hello WCF 和 WCF 轉送之間的主要差異在於該 hello 端點會公開 hello 定域機組中而不是在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="d71fa-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="d71fa-110">Hello 系列主題逐步在本教學課程之後，您必須執行中的服務和用戶端可叫用 hello hello 服務作業。</span><span class="sxs-lookup"><span data-stu-id="d71fa-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="d71fa-111">hello 第一個主題說明如何設定帳戶 tooset。</span><span class="sxs-lookup"><span data-stu-id="d71fa-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="d71fa-112">hello 接下來的步驟說明如何 toodefine 服務使用的合約、 如何 tooimplement hello 服務，以及如何 tooconfigure hello 程式碼中的服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="d71fa-113">這些主題亦說明如何 toohost 和執行 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="d71fa-114">hello 建立的服務是自我裝載且 hello 用戶端和服務上執行 hello 同一部電腦。</span><span class="sxs-lookup"><span data-stu-id="d71fa-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="d71fa-115">您可以使用程式碼或組態檔設定 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="d71fa-116">hello 最後三個步驟說明 toocreate 用戶端應用程式中，設定 hello 用戶端應用程式，並建立和使用用戶端可以存取的 hello 主機 hello 功能的方式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d71fa-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="d71fa-117">Prerequisites</span></span>

<span data-ttu-id="d71fa-118">toocomplete 本教學課程中，您必須遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="d71fa-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="d71fa-119">[Microsoft Visual Studio 2015 或更高版本](http://visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="d71fa-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="d71fa-120">本教學課程使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="d71fa-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="d71fa-121">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d71fa-121">An active Azure account.</span></span> <span data-ttu-id="d71fa-122">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="d71fa-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="d71fa-123">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="d71fa-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="d71fa-124">建立服務命名空間</span><span class="sxs-lookup"><span data-stu-id="d71fa-124">Create a service namespace</span></span>

<span data-ttu-id="d71fa-125">hello 第一個步驟是 toocreate 命名空間和 tooobtain[共用存取簽章 (SAS)](../service-bus-messaging/service-bus-sas.md)索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d71fa-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="d71fa-126">命名空間提供透過 hello 轉送服務公開的每個應用程式的應用程式界限。</span><span class="sxs-lookup"><span data-stu-id="d71fa-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="d71fa-127">當建立服務命名空間 SAS 金鑰會自動產生 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="d71fa-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="d71fa-128">服務命名空間和 SAS 金鑰 hello 結合 Azure tooauthenticate 存取 tooan 應用程式提供 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="d71fa-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="d71fa-129">請遵循 hello[這裡的指示](relay-create-namespace-portal.md)toocreate 轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="d71fa-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="d71fa-130">定義 WCF 服務合約</span><span class="sxs-lookup"><span data-stu-id="d71fa-130">Define a WCF service contract</span></span>

<span data-ttu-id="d71fa-131">hello 服務合約會指定哪些作業 （hello web 服務術語方法或函式） hello 服務支援。</span><span class="sxs-lookup"><span data-stu-id="d71fa-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="d71fa-132">合約可以透過定義 C++、C# 或 Visual Basic 介面建立。</span><span class="sxs-lookup"><span data-stu-id="d71fa-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="d71fa-133">Hello 介面中的每個方法對應 tooa 特定服務作業。</span><span class="sxs-lookup"><span data-stu-id="d71fa-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="d71fa-134">每個介面必須有 hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)屬性套用 tooit，而且每個作業都必須有 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit 套用的屬性。</span><span class="sxs-lookup"><span data-stu-id="d71fa-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="d71fa-135">如果其中有 hello 的介面中的方法[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)屬性並沒有 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx)屬性未公開該方法。</span><span class="sxs-lookup"><span data-stu-id="d71fa-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="d71fa-136">hello 範例 hello 程序中提供這些工作的 「 hello 」 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d71fa-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="d71fa-137">較大的合約和服務討論，請參閱[設計與實作服務](https://msdn.microsoft.com/library/ms729746.aspx)hello WCF 文件中。</span><span class="sxs-lookup"><span data-stu-id="d71fa-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="d71fa-138">使用介面建立轉送合約</span><span class="sxs-lookup"><span data-stu-id="d71fa-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="d71fa-139">系統管理員身分開啟 Visual Studio，以滑鼠右鍵按一下 [hello] 瀅蒰 hello**啟動**功能表，然後選取**系統管理員身分執行**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="d71fa-140">這會建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-140">Create a new console application project.</span></span> <span data-ttu-id="d71fa-141">按一下 hello**檔案**功能表，然後選取**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="d71fa-142">在 hello**新專案** 對話方塊中，按一下  **Visual C#** (如果**Visual C#**未出現，請查看 **其他語言**)。</span><span class="sxs-lookup"><span data-stu-id="d71fa-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="d71fa-143">按一下 hello**主控台應用程式 (.NET Framework)**範本，並將其命名**EchoService**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="d71fa-144">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="d71fa-145">安裝 hello 服務匯流排 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="d71fa-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="d71fa-146">此套件會自動將參考 toohello 服務匯流排程式庫，以及 hello WCF **System.ServiceModel**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="d71fa-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx)是 hello 命名空間，可讓您的 WCF 的 tooprogrammatically 存取 hello 基本功能。</span><span class="sxs-lookup"><span data-stu-id="d71fa-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="d71fa-148">服務匯流排會使用許多 hello 物件和屬性的 toodefine WCF 服務合約。</span><span class="sxs-lookup"><span data-stu-id="d71fa-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="d71fa-149">在 方案總管 hello 專案上按一下滑鼠右鍵，然後按一下**管理 NuGet 封裝...**.按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="d71fa-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="d71fa-150">確定該 hello 專案名稱已在 hello 選取**版本**方塊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="d71fa-151">按一下**安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="d71fa-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="d71fa-152">在 [方案總管] 中，按兩下 hello Program.cs 檔案 tooopen 它在 hello 編輯器中，如果它尚未開啟。</span><span class="sxs-lookup"><span data-stu-id="d71fa-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="d71fa-153">新增 hello 下列 using 陳述式在 hello hello 檔案最上方：</span><span class="sxs-lookup"><span data-stu-id="d71fa-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="d71fa-154">中的預設名稱變更 hello 命名空間名稱**EchoService**太**Microsoft.ServiceBus.Samples**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d71fa-155">本教學課程使用 hello C# 命名空間**Microsoft.ServiceBus.Samples**，這是 hello 命名空間的合約為基礎的 hello managed hello 中的 hello 設定檔中所使用的型別[設定 hello WCF 用戶端](#configure-the-wcf-client)步驟。</span><span class="sxs-lookup"><span data-stu-id="d71fa-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="d71fa-156">您可以指定當您建置這個範例中，任何命名的空間不過，hello 教學課程將無法運作，除非您修改 hello hello 合約和服務的命名空間，hello 應用程式組態檔中。</span><span class="sxs-lookup"><span data-stu-id="d71fa-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="d71fa-157">hello 命名空間中 hello App.config 檔案必須指定 hello 相同 hello C# 檔案中指定的命名空間。</span><span class="sxs-lookup"><span data-stu-id="d71fa-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="d71fa-158">直接在 hello 之後`Microsoft.ServiceBus.Samples`命名空間宣告，但 hello 命名空間中定義名為的新介面`IEchoContract`並套用 hello`ServiceContractAttribute`屬性 toohello 介面的命名空間值`http://samples.microsoft.com/ServiceModel/Relay/`。</span><span class="sxs-lookup"><span data-stu-id="d71fa-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="d71fa-159">hello 命名空間值不同於您在整個 hello 程式碼範圍內使用的 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="d71fa-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="d71fa-160">相反地，hello 命名空間值會當做此合約唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="d71fa-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="d71fa-161">明確指定 hello 命名空間，可防止 hello 預設命名空間值加入 toohello 合約名稱。</span><span class="sxs-lookup"><span data-stu-id="d71fa-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="d71fa-162">貼上下列程式碼 hello 命名空間宣告之後的 hello:</span><span class="sxs-lookup"><span data-stu-id="d71fa-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="d71fa-163">一般而言，hello 服務合約命名空間包含的命名配置，包括版本資訊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="d71fa-164">Hello 服務合約命名空間中包括版本資訊可以定義新的服務合約與新的命名空間，並將新的端點上公開的服務 tooisolate 主要變更。</span><span class="sxs-lookup"><span data-stu-id="d71fa-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="d71fa-165">這種方式，用戶端可以繼續 toouse hello 舊服務合約，而不需要 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="d71fa-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="d71fa-166">版本資訊可以包含日期或組建編號。</span><span class="sxs-lookup"><span data-stu-id="d71fa-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="d71fa-167">如需詳細資訊，請參閱[服務版本設定](http://go.microsoft.com/fwlink/?LinkID=180498)。</span><span class="sxs-lookup"><span data-stu-id="d71fa-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="d71fa-168">基於 hello 本教學課程，hello 命名 hello 服務合約命名空間的結構描述不包含版本資訊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="d71fa-169">Hello 內`IEchoContract`介面，請宣告 hello 單一作業 hello 方法`IEchoContract`hello 中的合約公開介面，並套用 hello`OperationContractAttribute`屬性 toohello 方法要做為一部分 tooexpose hello 公開的 WCF 轉送合約，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d71fa-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="d71fa-170">直接在 hello 之後`IEchoContract`介面定義中，宣告同時繼承自通道`IEchoContract`和也 toohello`IClientChannel`介面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d71fa-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="d71fa-171">通道是 hello 主機和用戶端用來傳遞資訊 tooeach 其他 hello WCF 物件。</span><span class="sxs-lookup"><span data-stu-id="d71fa-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="d71fa-172">稍後，您將撰寫 hello 通道 tooecho 資訊 hello 兩個應用程式之間的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d71fa-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="d71fa-173">從 hello**建置**功能表上，按一下 **建置方案**或按**Ctrl + Shift + B** tooconfirm hello 精確度的工作為止。</span><span class="sxs-lookup"><span data-stu-id="d71fa-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="d71fa-174">範例</span><span class="sxs-lookup"><span data-stu-id="d71fa-174">Example</span></span>

<span data-ttu-id="d71fa-175">下列程式碼的 hello 顯示定義的 WCF 轉送合約的基本介面。</span><span class="sxs-lookup"><span data-stu-id="d71fa-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="d71fa-176">Hello 已建立介面，您可以實作 hello 介面。</span><span class="sxs-lookup"><span data-stu-id="d71fa-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="d71fa-177">實作 hello WCF 合約</span><span class="sxs-lookup"><span data-stu-id="d71fa-177">Implement hello WCF contract</span></span>

<span data-ttu-id="d71fa-178">建立 Azure 的轉送，您必須先建立 hello 合約，它使用介面所定義。</span><span class="sxs-lookup"><span data-stu-id="d71fa-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="d71fa-179">如需有關建立 hello 介面的詳細資訊，請參閱 hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d71fa-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="d71fa-180">hello 下一個步驟是 tooimplement hello 介面。</span><span class="sxs-lookup"><span data-stu-id="d71fa-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="d71fa-181">這項作業包括建立類別，名為`EchoService`實作使用者定義的 hello`IEchoContract`介面。</span><span class="sxs-lookup"><span data-stu-id="d71fa-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="d71fa-182">實作 hello 介面之後，接著您設定 hello 介面使用 App.config 組態檔。</span><span class="sxs-lookup"><span data-stu-id="d71fa-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="d71fa-183">hello 設定檔包含 hello 應用程式，例如 hello hello 服務名稱、 hello 名稱 hello 合約和通訊協定都使用的 toocommunicate 與 hello 轉送服務的 hello 類型的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="d71fa-184">hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d71fa-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="d71fa-185">如需如何 tooimplement 服務合約的一般討論，請參閱[實作服務合約](https://msdn.microsoft.com/library/ms733764.aspx)hello WCF 文件中。</span><span class="sxs-lookup"><span data-stu-id="d71fa-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="d71fa-186">建立新的類別，名為`EchoService`的 hello 的 hello 定義之後，直接`IEchoContract`介面。</span><span class="sxs-lookup"><span data-stu-id="d71fa-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="d71fa-187">hello`EchoService`類別會實作 hello`IEchoContract`介面。</span><span class="sxs-lookup"><span data-stu-id="d71fa-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="d71fa-188">類似 tooother 介面實作，您可以實作 hello 定義不同的檔案中。</span><span class="sxs-lookup"><span data-stu-id="d71fa-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="d71fa-189">不過，本教學課程，hello 實作位於相同檔案做為 hello 介面定義，hello hello`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="d71fa-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="d71fa-190">套用 hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx)屬性 toohello`IEchoContract`介面。</span><span class="sxs-lookup"><span data-stu-id="d71fa-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="d71fa-191">hello 屬性會指定 hello 服務名稱和命名空間。</span><span class="sxs-lookup"><span data-stu-id="d71fa-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="d71fa-192">之後，請 hello`EchoService`類別會出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d71fa-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="d71fa-193">實作 hello`Echo`方法定義於 hello`IEchoContract`介面中 hello`EchoService`類別。</span><span class="sxs-lookup"><span data-stu-id="d71fa-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="d71fa-194">按一下**建置**，然後按一下 **建置方案**tooconfirm hello 精確度的工作。</span><span class="sxs-lookup"><span data-stu-id="d71fa-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="d71fa-195">定義 hello hello 服務主機的組態</span><span class="sxs-lookup"><span data-stu-id="d71fa-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="d71fa-196">hello 組態檔是非常類似 tooa WCF 組態檔。</span><span class="sxs-lookup"><span data-stu-id="d71fa-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="d71fa-197">它包含 hello 服務名稱、 端點 （也就是 hello 位置 Azure 轉送會公開為用戶端和主機彼此 toocommunicate），並 hello 繫結 （通訊協定都使用的 toocommunicate hello 類型）。</span><span class="sxs-lookup"><span data-stu-id="d71fa-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="d71fa-198">hello 主要差異在於此設定的服務端點會參考 tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding)繫結，這不是 hello.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="d71fa-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="d71fa-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding)是其中一個 hello hello 服務所定義的繫結。</span><span class="sxs-lookup"><span data-stu-id="d71fa-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="d71fa-200">在**方案總管 中**，按兩下 hello App.config 檔案 tooopen hello Visual Studio 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="d71fa-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="d71fa-201">在 hello `<appSettings>` hello 預留位置取代為您的服務命名空間中的 hello 名稱項目，和 hello 您在前述步驟中複製的 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="d71fa-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="d71fa-202">Hello 內`<system.serviceModel>`標記，加入`<services>`項目。</span><span class="sxs-lookup"><span data-stu-id="d71fa-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="d71fa-203">您可以在單一組態檔中定義多個轉送應用程式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="d71fa-204">不過，本教學課程只會定義一個。</span><span class="sxs-lookup"><span data-stu-id="d71fa-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="d71fa-205">在 hello`<services>`項目，加入`<service>`hello 服務項目 toodefine hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d71fa-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="d71fa-206">在 hello`<service>`項目，定義 hello 位置 hello 端點合約，並也 hello hello 端點的繫結型別。</span><span class="sxs-lookup"><span data-stu-id="d71fa-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="d71fa-207">hello 端點定義 hello 用戶端將在其中尋找 hello 主應用程式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="d71fa-208">稍後，hello 教學課程會使用此步驟 toocreate 完全公開透過 Azure 轉送 hello 主機的 URI。</span><span class="sxs-lookup"><span data-stu-id="d71fa-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="d71fa-209">hello 繫結宣告我們使用 TCP hello 與 hello 轉送服務的通訊協定 toocommunicate 如下。</span><span class="sxs-lookup"><span data-stu-id="d71fa-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="d71fa-210">從 hello**建置**功能表上，按一下 **建置方案**tooconfirm hello 精確度的工作。</span><span class="sxs-lookup"><span data-stu-id="d71fa-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="d71fa-211">範例</span><span class="sxs-lookup"><span data-stu-id="d71fa-211">Example</span></span>

<span data-ttu-id="d71fa-212">hello 下列程式碼顯示 hello hello 服務合約實作。</span><span class="sxs-lookup"><span data-stu-id="d71fa-212">hello following code shows hello implementation of hello service contract.</span></span>

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

<span data-ttu-id="d71fa-213">hello 下列程式碼顯示 hello hello 與 hello 服務主機相關聯的 App.config 檔案的基本格式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="d71fa-214">裝載和執行基本 web 服務 tooregister 與 hello 轉送服務</span><span class="sxs-lookup"><span data-stu-id="d71fa-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="d71fa-215">此步驟說明如何 toorun Azure 轉送服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="d71fa-216">建立 hello 轉送認證</span><span class="sxs-lookup"><span data-stu-id="d71fa-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="d71fa-217">在`Main()`、 哪些 toostore hello 命名空間中建立兩個變數和 hello 從 hello 主控台視窗讀取的 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="d71fa-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="d71fa-218">hello SAS 金鑰將會使用更新版本的 tooaccess 您的專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="d71fa-219">hello 命名空間會當做參數傳遞太`CreateServiceUri`toocreate 服務 URI。</span><span class="sxs-lookup"><span data-stu-id="d71fa-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="d71fa-220">使用[TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior)物件，宣告您將使用 SAS 金鑰作為 hello 認證類型。</span><span class="sxs-lookup"><span data-stu-id="d71fa-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="d71fa-221">新增下列程式碼直接在 hello hello 最後一個步驟中加入的程式碼之後的 hello。</span><span class="sxs-lookup"><span data-stu-id="d71fa-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="d71fa-222">建立 hello 服務的基底地址</span><span class="sxs-lookup"><span data-stu-id="d71fa-222">Create a base address for hello service</span></span>

<span data-ttu-id="d71fa-223">Hello hello 最後一個步驟中加入程式碼之後, 建立`Uri`hello 基底地址的 hello 服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d71fa-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="d71fa-224">此 URI 指定 hello Service Bus 配置、 hello 命名空間及 hello 路徑 hello 服務介面。</span><span class="sxs-lookup"><span data-stu-id="d71fa-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="d71fa-225">「 sb 」 hello Service Bus 配置的縮寫，表示我們使用 TCP 做為 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d71fa-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="d71fa-226">這也先前已指出 hello 組態檔中，當[NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx)被指定為 hello 繫結。</span><span class="sxs-lookup"><span data-stu-id="d71fa-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="d71fa-227">此教學課程，hello URI 是`sb://putServiceNamespaceHere.windows.net/EchoService`。</span><span class="sxs-lookup"><span data-stu-id="d71fa-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="d71fa-228">建立及設定 hello 服務主機</span><span class="sxs-lookup"><span data-stu-id="d71fa-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="d71fa-229">Hello 連線模式設定太`AutoDetect`。</span><span class="sxs-lookup"><span data-stu-id="d71fa-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="d71fa-230">hello 連線模式可描述 hello 通訊協定 hello 服務會使用 toocommunicate 與 hello 轉送服務。HTTP 或 TCP。</span><span class="sxs-lookup"><span data-stu-id="d71fa-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="d71fa-231">使用 hello 預設設定`AutoDetect`，hello 服務會嘗試透過 TCP，如果有的話和 HTTP tooconnect tooAzure 轉送如果無法使用 TCP。</span><span class="sxs-lookup"><span data-stu-id="d71fa-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="d71fa-232">請注意，這不同於 hello 通訊協定 hello 服務指定用戶端通訊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="d71fa-233">使用 hello 繫結會判斷該通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d71fa-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="d71fa-234">例如，服務可以使用 hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx)繫結，這會指定，其端點與用戶端透過 HTTP 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="d71fa-235">相同服務可以指定**ConnectivityMode.AutoDetect**以便 hello 服務與 Azure 轉送透過 TCP 通訊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="d71fa-236">建立 hello 服務主機，請使用本節稍早建立 URI 的 hello。</span><span class="sxs-lookup"><span data-stu-id="d71fa-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="d71fa-237">具現化 hello 服務的 hello WCF 物件 hello 服務主機。</span><span class="sxs-lookup"><span data-stu-id="d71fa-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="d71fa-238">在這裡，您將它傳遞 hello 類型的服務，您想 toocreate (`EchoService`類型)，和也想 tooexpose hello 服務 toohello 位址。</span><span class="sxs-lookup"><span data-stu-id="d71fa-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="d71fa-239">在 hello hello Program.cs 檔案頂端，加入參考太[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx)和[Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description)。</span><span class="sxs-lookup"><span data-stu-id="d71fa-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="d71fa-240">回到`Main()`，設定 hello 端點 tooenable 公用存取。</span><span class="sxs-lookup"><span data-stu-id="d71fa-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="d71fa-241">此步驟會通知 hello 轉送服務，您的應用程式即可公開找到藉由檢查專案的 hello ATOM 摘要。</span><span class="sxs-lookup"><span data-stu-id="d71fa-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="d71fa-242">如果您設定**DiscoveryType**太**私人**，用戶端仍將是無法 tooaccess hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="d71fa-243">不過，hello 服務不會出現搜尋 hello 轉送命名空間時。</span><span class="sxs-lookup"><span data-stu-id="d71fa-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="d71fa-244">相反地，hello 用戶端會事先有 tooknow hello 端點路徑。</span><span class="sxs-lookup"><span data-stu-id="d71fa-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="d71fa-245">套用 hello 服務認證 toohello hello App.config 檔案中定義的服務端點：</span><span class="sxs-lookup"><span data-stu-id="d71fa-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="d71fa-246">Hello 上一個步驟所述，您無法宣告多個服務和 hello 組態檔中的端點。</span><span class="sxs-lookup"><span data-stu-id="d71fa-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="d71fa-247">如果您在這段程式碼會周遊 hello 組態檔案，並搜尋針對每個端點 toowhich 應套用您的認證。</span><span class="sxs-lookup"><span data-stu-id="d71fa-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="d71fa-248">不過，本教學課程，hello 設定檔有只有一個端點。</span><span class="sxs-lookup"><span data-stu-id="d71fa-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="d71fa-249">開啟 hello 服務主機</span><span class="sxs-lookup"><span data-stu-id="d71fa-249">Open hello service host</span></span>

1. <span data-ttu-id="d71fa-250">開啟 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="d71fa-251">通知 hello 服務的 hello 使用者執行，並且說明如何關閉 hello 服務 tooshut。</span><span class="sxs-lookup"><span data-stu-id="d71fa-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="d71fa-252">完成後，關閉 hello 服務主機。</span><span class="sxs-lookup"><span data-stu-id="d71fa-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="d71fa-253">按**Ctrl + Shift + B** toobuild hello 專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="d71fa-254">範例</span><span class="sxs-lookup"><span data-stu-id="d71fa-254">Example</span></span>

<span data-ttu-id="d71fa-255">完整的服務程式碼應如下所示。</span><span class="sxs-lookup"><span data-stu-id="d71fa-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="d71fa-256">hello 程式碼包含 hello 服務合約和實作，從上一個步驟中 hello 教學課程中，並裝載 hello 主控台應用程式中的服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

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

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="d71fa-257">建立 hello 服務合約的 WCF 用戶端</span><span class="sxs-lookup"><span data-stu-id="d71fa-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="d71fa-258">hello 下一個步驟是 toocreate 用戶端應用程式，並定義 hello 服務合約，您將在稍後步驟中實作。</span><span class="sxs-lookup"><span data-stu-id="d71fa-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="d71fa-259">請注意，其中許多步驟類似於 hello 步驟使用 toocreate 服務： 定義合約、 編輯 App.config 檔案，使用認證 tooconnect toohello 轉送服務，以此類推。</span><span class="sxs-lookup"><span data-stu-id="d71fa-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="d71fa-260">hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d71fa-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="d71fa-261">執行下列 hello hello 用戶端 hello 目前 Visual Studio 方案中建立新的專案：</span><span class="sxs-lookup"><span data-stu-id="d71fa-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="d71fa-262">在 方案總管在 hello 相同的方案，其中包含 hello 服務，hello 目前的方案 （不 hello 專案），以滑鼠右鍵按一下，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="d71fa-263">然後按一下新增專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="d71fa-264">在 hello**加入新的專案**對話方塊中，按一下  **Visual C#** (如果**Visual C#**未出現，請查看 **其他語言**)，請選取 hello**主控台應用程式 (.NET Framework)**範本，並將其命名**EchoClient**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="d71fa-265">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d71fa-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="d71fa-266">在 [方案總管] 中，按兩下 hello Program.cs 檔案中 hello **EchoClient** tooopen 它在 hello 編輯器中，如果還沒有開啟的專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="d71fa-267">中的預設名稱變更 hello 命名空間名稱`EchoClient`太`Microsoft.ServiceBus.Samples`。</span><span class="sxs-lookup"><span data-stu-id="d71fa-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="d71fa-268">安裝 hello[服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)： 在方案總管 中，以滑鼠右鍵按一下 hello **EchoClient**專案，然後再按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="d71fa-269">按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="d71fa-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="d71fa-270">按一下**安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="d71fa-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="d71fa-271">新增`using`hello 陳述式[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello Program.cs 檔案中的命名空間。</span><span class="sxs-lookup"><span data-stu-id="d71fa-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="d71fa-272">加入 hello 服務合約定義 toohello 命名空間，hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d71fa-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="d71fa-273">請注意，這個定義是相同的 toohello 定義用於 hello**服務**專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="d71fa-274">您應該在 hello hello 最上方加入下列程式碼`Microsoft.ServiceBus.Samples`命名空間。</span><span class="sxs-lookup"><span data-stu-id="d71fa-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="d71fa-275">按**Ctrl + Shift + B** toobuild hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d71fa-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="d71fa-276">範例</span><span class="sxs-lookup"><span data-stu-id="d71fa-276">Example</span></span>

<span data-ttu-id="d71fa-277">hello 下列程式碼顯示 hello 目前狀態的 hello Program.cs 檔案中 hello **EchoClient**專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

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

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="d71fa-278">Hello WCF 用戶端設定</span><span class="sxs-lookup"><span data-stu-id="d71fa-278">Configure hello WCF client</span></span>

<span data-ttu-id="d71fa-279">在此步驟中，您可以建立的 App.config 檔案，存取先前在本教學課程中建立的 hello 服務的基本用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="d71fa-280">此 App.config 檔案定義 hello 合約、 繫結和 hello 端點的名稱。</span><span class="sxs-lookup"><span data-stu-id="d71fa-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="d71fa-281">hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d71fa-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="d71fa-282">在 方案總管中 hello **EchoClient**專案中，按兩下**App.config** tooopen hello Visual Studio 編輯器中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="d71fa-283">在 hello `<appSettings>` hello 預留位置取代為您的服務命名空間中的 hello 名稱項目，和 hello 您在前述步驟中複製的 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="d71fa-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="d71fa-284">在 hello system.serviceModel 項目，將新增`<client>`項目。</span><span class="sxs-lookup"><span data-stu-id="d71fa-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="d71fa-285">此步驟宣告您正在定義 WCF 樣式的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="d71fa-286">在 hello`client`項目，定義 hello 名稱、 合約和 hello 端點的繫結型別。</span><span class="sxs-lookup"><span data-stu-id="d71fa-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="d71fa-287">此步驟定義 hello hello 端點，且定義為 hello 服務和 hello 事實 hello 用戶端應用程式會使用與 Azure 轉送 TCP toocommunicate hello 合約名稱。</span><span class="sxs-lookup"><span data-stu-id="d71fa-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="d71fa-288">hello 端點的名稱會在 hello 下一步 toolink hello 服務 URI 與此端點組態。</span><span class="sxs-lookup"><span data-stu-id="d71fa-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="d71fa-289">按一下 [檔案]，然後按一下 [全部儲存]。</span><span class="sxs-lookup"><span data-stu-id="d71fa-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="d71fa-290">範例</span><span class="sxs-lookup"><span data-stu-id="d71fa-290">Example</span></span>

<span data-ttu-id="d71fa-291">hello 下列程式碼顯示 hello hello Echo 用戶端的 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-291">hello following code shows hello App.config file for hello Echo client.</span></span>

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

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="d71fa-292">實作 hello WCF 用戶端</span><span class="sxs-lookup"><span data-stu-id="d71fa-292">Implement hello WCF client</span></span>
<span data-ttu-id="d71fa-293">在此步驟中，您可以實作基本用戶端應用程式存取您先前在本教學課程中建立的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="d71fa-294">Hello 用戶端執行許多 hello 類似 toohello 服務時，相同作業 tooaccess Azure 轉送：</span><span class="sxs-lookup"><span data-stu-id="d71fa-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="d71fa-295">設定 hello 連線模式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="d71fa-296">建立 hello 找出 hello 主機服務的 URI。</span><span class="sxs-lookup"><span data-stu-id="d71fa-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="d71fa-297">定義 hello 安全性認證。</span><span class="sxs-lookup"><span data-stu-id="d71fa-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="d71fa-298">適用於 hello 認證 toohello 連接。</span><span class="sxs-lookup"><span data-stu-id="d71fa-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="d71fa-299">開啟 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="d71fa-299">Opens hello connection.</span></span>
6. <span data-ttu-id="d71fa-300">執行 hello 應用程式特定的工作。</span><span class="sxs-lookup"><span data-stu-id="d71fa-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="d71fa-301">關閉 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="d71fa-301">Closes hello connection.</span></span>

<span data-ttu-id="d71fa-302">不過，其中一個 hello 主要差異是 hello 用戶端應用程式會使用通道 tooconnect toohello 轉送服務，而 hello 服務會使用呼叫太**ServiceHost**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="d71fa-303">hello 範例 hello 程序中，會提供用於這些工作的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d71fa-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="d71fa-304">實作用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="d71fa-304">Implement a client application</span></span>
1. <span data-ttu-id="d71fa-305">Hello 連線模式設定太**自動偵測**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="d71fa-306">新增下列程式碼內 hello hello`Main()`方法 hello **EchoClient**應用程式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="d71fa-307">定義變數 toohold hello hello 服務命名空間，以及 SAS 金鑰的值從 hello 主控台讀取的。</span><span class="sxs-lookup"><span data-stu-id="d71fa-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="d71fa-308">建立 hello 轉送專案中定義的 hello 主機的 hello 位置的 URI。</span><span class="sxs-lookup"><span data-stu-id="d71fa-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="d71fa-309">建立服務命名空間端點 hello 認證物件。</span><span class="sxs-lookup"><span data-stu-id="d71fa-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="d71fa-310">建立 hello 通道處理站載入 hello hello App.config 檔案中所述的組態。</span><span class="sxs-lookup"><span data-stu-id="d71fa-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="d71fa-311">通道處理站會建立的通道，透過此 hello 服務與用戶端應用程式進行通訊的 WCF 物件。</span><span class="sxs-lookup"><span data-stu-id="d71fa-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="d71fa-312">套用 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="d71fa-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="d71fa-313">建立並開啟 hello 通道 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="d71fa-314">撰寫 hello 基本使用者介面與 hello 回應的功能。</span><span class="sxs-lookup"><span data-stu-id="d71fa-314">Write hello basic user interface and functionality for hello echo.</span></span>

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

    <span data-ttu-id="d71fa-315">請注意，hello 程式碼使用 hello hello 通道物件執行個體做為 proxy hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d71fa-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="d71fa-316">關閉 hello 通道和關閉 hello factory。</span><span class="sxs-lookup"><span data-stu-id="d71fa-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="d71fa-317">範例</span><span class="sxs-lookup"><span data-stu-id="d71fa-317">Example</span></span>

<span data-ttu-id="d71fa-318">您已完成的程式碼應該會出現，如下所示，顯示如何 toocreate 用戶端應用程式、 toocall hello hello 服務作業的方式和 tooclose hello 作業之後所 hello 的用戶端呼叫已完成。</span><span class="sxs-lookup"><span data-stu-id="d71fa-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

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

## <a name="run-hello-applications"></a><span data-ttu-id="d71fa-319">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d71fa-319">Run hello applications</span></span>

1. <span data-ttu-id="d71fa-320">按**Ctrl + Shift + B** toobuild hello 方案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="d71fa-321">這會建置 hello 用戶端專案和 hello hello 先前步驟中建立的服務專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="d71fa-322">之前執行的 hello 用戶端應用程式，您必須確定 hello 服務應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="d71fa-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="d71fa-323">在 Visual Studio 中的方案總管] 中以滑鼠右鍵按一下 hello **EchoService**方案，然後按一下 [**屬性**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="d71fa-324">在 [hello 方案內容] 對話方塊中按一下**啟始專案**，然後按一下 [hello**多個啟始專案**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d71fa-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="d71fa-325">請確定**EchoService** hello 清單中第一個出現。</span><span class="sxs-lookup"><span data-stu-id="d71fa-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="d71fa-326">設定 hello**動作**方塊這兩個 hello **EchoService**和**EchoClient**太專案**啟動**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="d71fa-327">按一下 [專案相依性]。</span><span class="sxs-lookup"><span data-stu-id="d71fa-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="d71fa-328">在 hello**專案**方塊中，選取**EchoClient**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="d71fa-329">在 hello**取決於**方塊中，請確定**EchoService**已核取。</span><span class="sxs-lookup"><span data-stu-id="d71fa-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="d71fa-330">按一下**確定**toodismiss hello**屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="d71fa-331">按**F5** toorun 這兩個專案。</span><span class="sxs-lookup"><span data-stu-id="d71fa-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="d71fa-332">兩個主控台視窗開啟，並提示您輸入 hello 命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="d71fa-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="d71fa-333">hello 服務必須先執行，所以在 hello **EchoService**主控台視窗中，輸入 hello 命名空間，然後按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="d71fa-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="d71fa-334">接下來，系統會提示您輸入 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="d71fa-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="d71fa-335">輸入 hello SAS 金鑰，然後按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="d71fa-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="d71fa-336">以下是 hello 主控台視窗的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="d71fa-336">Here is example output from hello console window.</span></span> <span data-ttu-id="d71fa-337">請注意以下是僅限用途，例如提供 hello 值。</span><span class="sxs-lookup"><span data-stu-id="d71fa-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="d71fa-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="d71fa-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="d71fa-339">hello 服務應用程式列印 toohello 主控台視窗 hello 它會接聽的位址，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d71fa-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="d71fa-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="d71fa-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="d71fa-341">在 hello **EchoClient**主控台視窗中，輸入 hello hello 服務應用程式先前輸入的相同資訊。</span><span class="sxs-lookup"><span data-stu-id="d71fa-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="d71fa-342">請依照上一個步驟 tooenter hello hello 相同的服務命名空間和 SAS 金鑰 hello 用戶端應用程式的值。</span><span class="sxs-lookup"><span data-stu-id="d71fa-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="d71fa-343">輸入這些值之後, hello 用戶端通道 toohello 服務就會開啟，並提示您 tooenter 一些文字，如 hello 下列主控台輸出範例所示。</span><span class="sxs-lookup"><span data-stu-id="d71fa-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="d71fa-344">輸入一些文字 toosend toohello 服務應用程式，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="d71fa-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="d71fa-345">此文字會傳送 toohello 服務透過 hello Echo 服務作業，並會出現在 hello 服務主控台視窗，如下列範例輸出的 hello 所示。</span><span class="sxs-lookup"><span data-stu-id="d71fa-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="d71fa-346">hello 用戶端應用程式收到 hello 傳回值的 hello`Echo`作業，因為它是原始的 hello 文字，並將它列印 tooits 主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="d71fa-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="d71fa-347">hello 以下是 hello 用戶端主控台視窗的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="d71fa-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="d71fa-348">您可以繼續從這種方式中的 hello 用戶端 toohello 服務傳送文字訊息。</span><span class="sxs-lookup"><span data-stu-id="d71fa-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="d71fa-349">當您完成時，按 Enter 鍵 hello 用戶端和服務主控台視窗 tooend 中兩個應用程式。</span><span class="sxs-lookup"><span data-stu-id="d71fa-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d71fa-350">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d71fa-350">Next steps</span></span>

<span data-ttu-id="d71fa-351">本教學課程示範了如何 toobuild Azure 轉接用戶端應用程式和服務使用 hello 的服務匯流排的 WCF 轉送功能。</span><span class="sxs-lookup"><span data-stu-id="d71fa-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="d71fa-352">如需使用[服務匯流排通訊](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)的類似教學課程，請參閱[開始使用服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="d71fa-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="d71fa-353">toolearn 深入了解 Azure 轉送，請參閱下列主題中的 hello。</span><span class="sxs-lookup"><span data-stu-id="d71fa-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="d71fa-354">Azure 服務匯流排架構概觀</span><span class="sxs-lookup"><span data-stu-id="d71fa-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="d71fa-355">Azure 轉送概觀</span><span class="sxs-lookup"><span data-stu-id="d71fa-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="d71fa-356">如何 toouse hello WCF 轉送服務的.NET</span><span class="sxs-lookup"><span data-stu-id="d71fa-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
