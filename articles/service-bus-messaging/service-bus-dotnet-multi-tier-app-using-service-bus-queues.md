---
title: "使用 Azure 服務匯流排的 .NET 多層應用程式 | Microsoft Docs"
description: "協助您在 Azure 中開發多層式應用程式，以使用服務匯流排佇列在各層之間進行通訊的 .NET 教學課程。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 8b502f5ac5d89801d390a872e7a8b06e094ecbba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="0e66e-103">使用 Azure 服務匯流排佇列的 .NET 多層應用程式</span><span class="sxs-lookup"><span data-stu-id="0e66e-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="0e66e-104">簡介</span><span class="sxs-lookup"><span data-stu-id="0e66e-104">Introduction</span></span>
<span data-ttu-id="0e66e-105">使用 Visual Studio 和免費 Azure SDK for .NET 開發 Microsoft Azure 很容易。</span><span class="sxs-lookup"><span data-stu-id="0e66e-105">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span></span> <span data-ttu-id="0e66e-106">本教學課程將逐步引導您完成相關步驟，以建立在本機環境中執行、使用多個 Azure 資源的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e66e-106">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="0e66e-107">您將了解下列內容：</span><span class="sxs-lookup"><span data-stu-id="0e66e-107">You will learn the following:</span></span>

* <span data-ttu-id="0e66e-108">如何透過單一下載和安裝，讓電腦適合用於進行 Azure 開發。</span><span class="sxs-lookup"><span data-stu-id="0e66e-108">How to enable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="0e66e-109">如何使用 Visual Studio 進行 Azure 相關開發。</span><span class="sxs-lookup"><span data-stu-id="0e66e-109">How to use Visual Studio to develop for Azure.</span></span>
* <span data-ttu-id="0e66e-110">如何使用 Web 與背景工作角色，在 Azure 建立多層式應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e66e-110">How to create a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="0e66e-111">如何使用服務匯流排佇列在階層間通訊。</span><span class="sxs-lookup"><span data-stu-id="0e66e-111">How to communicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="0e66e-112">在本教學課程中，您將在 Azure 雲端服務中建置和執行多層式應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e66e-112">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="0e66e-113">前端為 ASP.NET MVC Web 角色，而後端為使用服務匯流排佇列的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="0e66e-113">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="0e66e-114">您可以建立相同的多層應用程式，並使其前端作為部署至 Azure 網站而非雲端服務的 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="0e66e-114">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span></span> <span data-ttu-id="0e66e-115">您也可以試試 [.NET 內部部署/雲端混合式應用程式](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="0e66e-115">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="0e66e-116">下列螢幕擷取畫面顯示完成的應用程式：</span><span class="sxs-lookup"><span data-stu-id="0e66e-116">The following screen shot shows the completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="0e66e-117">案例概觀：內部角色通訊</span><span class="sxs-lookup"><span data-stu-id="0e66e-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="0e66e-118">為了提交訂單進行處理，Web 角色中執行的前端 UI 元件必須與背景工作角色中執行的中間層互動。</span><span class="sxs-lookup"><span data-stu-id="0e66e-118">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span></span> <span data-ttu-id="0e66e-119">此範例使用服務匯流排傳訊在各層之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="0e66e-119">This example uses Service Bus messaging for the communication between the tiers.</span></span>

<span data-ttu-id="0e66e-120">在 Web 層與中間層之間使用服務匯流排傳訊，可使這兩個元件彼此脫鉤。</span><span class="sxs-lookup"><span data-stu-id="0e66e-120">Using Service Bus messaging between the web and middle tiers decouples the two components.</span></span> <span data-ttu-id="0e66e-121">相較於直接傳訊 (亦即，TCP 或 HTTP)，Web 層不會直接連線至中間層，而是透過訊息的形式，將工作單位推播至服務匯流排，而後者會可靠地保管工作單位，直到中間層準備好取用並處理這些工作單位為止。</span><span class="sxs-lookup"><span data-stu-id="0e66e-121">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span></span>

<span data-ttu-id="0e66e-122">服務匯流排提供兩個實體來支援代理的傳訊，也就是：佇列和主題。</span><span class="sxs-lookup"><span data-stu-id="0e66e-122">Service Bus provides two entities to support brokered messaging: queues and topics.</span></span> <span data-ttu-id="0e66e-123">使用佇列時，每個傳送至佇列的訊息都是由單一接收者取用。</span><span class="sxs-lookup"><span data-stu-id="0e66e-123">With queues, each message sent to the queue is consumed by a single receiver.</span></span> <span data-ttu-id="0e66e-124">主題可支援發佈/訂用帳戶模式，亦即每個發佈的訊息會提供給在主題註冊的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e66e-124">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span></span> <span data-ttu-id="0e66e-125">每個訂閱在邏輯上會維護自己的訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="0e66e-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="0e66e-126">訂用帳戶也可以設定成使用篩選規則，以將傳遞至訂用帳戶佇列的訊息限制為符合篩選條件的訊息。</span><span class="sxs-lookup"><span data-stu-id="0e66e-126">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span></span> <span data-ttu-id="0e66e-127">下列範例使用服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="0e66e-127">The following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="0e66e-128">此通訊機制具有數個超越直接傳訊的優點：</span><span class="sxs-lookup"><span data-stu-id="0e66e-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="0e66e-129">**暫時分離。**</span><span class="sxs-lookup"><span data-stu-id="0e66e-129">**Temporal decoupling.**</span></span> <span data-ttu-id="0e66e-130">使用非同步傳訊模式時，生產者和取用者不需要同時處於線上狀態。</span><span class="sxs-lookup"><span data-stu-id="0e66e-130">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span></span> <span data-ttu-id="0e66e-131">服務匯流排會可靠地保管訊息，直到取用方準備好接收訊息為止。</span><span class="sxs-lookup"><span data-stu-id="0e66e-131">Service Bus reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="0e66e-132">如此一來，分散式應用程式的元件即使中斷連線 (例如，基於維護原因而計劃性中斷，或基於元件損毀而意外中斷)，也不會影響整體系統。</span><span class="sxs-lookup"><span data-stu-id="0e66e-132">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="0e66e-133">此外，取用方應用程式只需要在一天中的特定時間處於線上狀態即可。</span><span class="sxs-lookup"><span data-stu-id="0e66e-133">Furthermore, the consuming application might only need to come online during certain times of the day.</span></span>
* <span data-ttu-id="0e66e-134">**負載調節。**</span><span class="sxs-lookup"><span data-stu-id="0e66e-134">**Load leveling.**</span></span> <span data-ttu-id="0e66e-135">在許多應用程式中，系統負載會隨時間改變，而處理每個工作單位所需的時間卻通常固定不變。</span><span class="sxs-lookup"><span data-stu-id="0e66e-135">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="0e66e-136">有佇列作為訊息生產者與取用者之間的中間者後，就只需佈建取用方應用程式 (背景工作) 來容納平均負載而非尖峰負載。</span><span class="sxs-lookup"><span data-stu-id="0e66e-136">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span></span> <span data-ttu-id="0e66e-137">佇列的深度會隨著連入負載的改變而增加和縮短。</span><span class="sxs-lookup"><span data-stu-id="0e66e-137">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="0e66e-138">就處理應用程式負載所需的基礎結構數量而言，如此可直接節省金錢。</span><span class="sxs-lookup"><span data-stu-id="0e66e-138">This directly saves money in terms of the amount of infrastructure required to service the application load.</span></span>
* <span data-ttu-id="0e66e-139">**負載平衡。**</span><span class="sxs-lookup"><span data-stu-id="0e66e-139">**Load balancing.**</span></span> <span data-ttu-id="0e66e-140">當負載增加時，可以新增更多的背景工作程序來讀取佇列中的訊息。</span><span class="sxs-lookup"><span data-stu-id="0e66e-140">As load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="0e66e-141">每個訊息僅由其中一個背景工作程序處理。</span><span class="sxs-lookup"><span data-stu-id="0e66e-141">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="0e66e-142">此外，這個提取型負載平衡機制可讓背景工作電腦獲得最佳利用，即使背景工作電腦的處理能力有所不同也一樣，因為背景工作電腦將以自己的最大速率提取訊息。</span><span class="sxs-lookup"><span data-stu-id="0e66e-142">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="0e66e-143">此模式通常稱為「競爭取用者」模式。</span><span class="sxs-lookup"><span data-stu-id="0e66e-143">This pattern is often termed the *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="0e66e-144">下列幾節討論實作此架構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0e66e-144">The following sections discuss the code that implements this architecture.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="0e66e-145">設定開發環境</span><span class="sxs-lookup"><span data-stu-id="0e66e-145">Set up the development environment</span></span>
<span data-ttu-id="0e66e-146">在開始開發 Azure 應用程式之前，請取得工具，並設定開發環境：</span><span class="sxs-lookup"><span data-stu-id="0e66e-146">Before you can begin developing Azure applications, get the tools and set up your development environment.</span></span>

1. <span data-ttu-id="0e66e-147">從 SDK [下載頁面](https://azure.microsoft.com/downloads/)安裝 Azure SDK for .NET。</span><span class="sxs-lookup"><span data-stu-id="0e66e-147">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="0e66e-148">在 **.NET** 資料行中，按一下您所使用的 [Visual Studio](http://www.visualstudio.com) 版本。</span><span class="sxs-lookup"><span data-stu-id="0e66e-148">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="0e66e-149">本教學課程中的步驟使用 Visual Studio 2015，但也可使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="0e66e-149">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="0e66e-150">當系統提示您執行或儲存安裝程式時，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-150">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="0e66e-151">在 **Web Platform Installer** 中，按一下 [安裝] 並繼續進行安裝。</span><span class="sxs-lookup"><span data-stu-id="0e66e-151">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="0e66e-152">完成安裝後，您將具有開始進行開發所需的一切。</span><span class="sxs-lookup"><span data-stu-id="0e66e-152">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="0e66e-153">SDK 包含可讓您在 Visual Studio 輕易開發 Azure 應用程式的工具。</span><span class="sxs-lookup"><span data-stu-id="0e66e-153">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="0e66e-154">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="0e66e-154">Create a namespace</span></span>
<span data-ttu-id="0e66e-155">下一步是建立服務命名空間，並取得共用存取簽章 (SAS) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e66e-155">The next step is to create a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="0e66e-156">命名空間會為每個透過服務匯流排公開的應用程式提供應用程式界限。</span><span class="sxs-lookup"><span data-stu-id="0e66e-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="0e66e-157">建立命名空間時，系統會產生 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e66e-157">A SAS key is generated by the system when a namespace is created.</span></span> <span data-ttu-id="0e66e-158">命名空間與 SAS 金鑰的結合提供一個認證，供服務匯流排驗證對應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="0e66e-158">The combination of namespace and SAS key provides the credentials for Service Bus to authenticate access to an application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="0e66e-159">建立 Web 角色</span><span class="sxs-lookup"><span data-stu-id="0e66e-159">Create a web role</span></span>
<span data-ttu-id="0e66e-160">在本節中，您會建置應用程式的前端。</span><span class="sxs-lookup"><span data-stu-id="0e66e-160">In this section, you build the front end of your application.</span></span> <span data-ttu-id="0e66e-161">首先，您會建立應用程式顯示的頁面。</span><span class="sxs-lookup"><span data-stu-id="0e66e-161">First, you create the pages that your application displays.</span></span>
<span data-ttu-id="0e66e-162">之後，新增程式碼以提交項目給服務匯流排佇列，並顯示佇列的狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="0e66e-162">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="0e66e-163">建立專案</span><span class="sxs-lookup"><span data-stu-id="0e66e-163">Create the project</span></span>
1. <span data-ttu-id="0e66e-164">使用系統管理員權限啟動 Visual Studio：在 **Visual Studio** 程式圖示上按一下滑鼠右鍵，然後按一下 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-164">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="0e66e-165">這篇文章稍後討論的 Azure 計算模擬器需要 Visual Studio 以系統管理員權限啟動。</span><span class="sxs-lookup"><span data-stu-id="0e66e-165">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="0e66e-166">在 Visual Studio 的 [檔案] 功能表，按一下 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-166">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="0e66e-167">從 [已安裝的範本] 的 [Visual C#] 下，按一下 [雲端]，然後按一下 [Azure 雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="0e66e-168">將專案命名為 **MultiTierApp**。</span><span class="sxs-lookup"><span data-stu-id="0e66e-168">Name the project **MultiTierApp**.</span></span> <span data-ttu-id="0e66e-169">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0e66e-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="0e66e-170">從 **.NET Framework 4.5** 角色中，按兩下 [ASP.NET Web 角色]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="0e66e-171">將滑鼠移至 [Azure 雲端服務解決方案] 下的 [WebRole1]，按一下鉛筆圖示，將 Web 角色重新命名為 **FrontendWebRole**。</span><span class="sxs-lookup"><span data-stu-id="0e66e-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span></span> <span data-ttu-id="0e66e-172">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0e66e-172">Then click **OK**.</span></span> <span data-ttu-id="0e66e-173">(請確定您輸入 "Frontend"，其中 e 為小寫，而不是 "FrontEnd"。)</span><span class="sxs-lookup"><span data-stu-id="0e66e-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="0e66e-174">在 [新增 ASP.NET 專案] 對話方塊的 [選取範本] 清單中，按一下 [MVC]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-174">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="0e66e-175">還是在 [新增 ASP.NET 專案] 對話方塊中，按一下 [變更驗證] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e66e-175">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span></span> <span data-ttu-id="0e66e-176">在 [變更驗證] 對話方塊中，按一下 [不需要驗證]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-176">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="0e66e-177">在本教學課程中，您會部署不需要使用者登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e66e-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="0e66e-178">回到 [新增 ASP.NET 專案] 對話方塊中，按一下 [確定] 以建立專案。</span><span class="sxs-lookup"><span data-stu-id="0e66e-178">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span></span>
8. <span data-ttu-id="0e66e-179">在 [方案總管] 的 [FrontendWebRole] 專案中，以滑鼠右鍵按一下 [參考]，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-179">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="0e66e-180">按一下 [瀏覽] 索引標籤，然後搜尋 `Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="0e66e-180">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="0e66e-181">選取 **WindowsAzure.ServiceBus** 套件，按一下 [安裝]，然後接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="0e66e-181">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="0e66e-182">請注意，現在已參考必要的用戶端組件，並已新增一些新的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="0e66e-182">Note that the required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="0e66e-183">在 [方案總管] 中，於 [模型] 上按一下滑鼠右鍵、按一下 [新增]，再按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="0e66e-184">在 [名稱] 方塊中，輸入名稱 **OnlineOrder.cs**。</span><span class="sxs-lookup"><span data-stu-id="0e66e-184">In the **Name** box, type the name **OnlineOrder.cs**.</span></span> <span data-ttu-id="0e66e-185">然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-185">Then click **Add**.</span></span>

### <a name="write-the-code-for-your-web-role"></a><span data-ttu-id="0e66e-186">撰寫 Web 角色的程式碼</span><span class="sxs-lookup"><span data-stu-id="0e66e-186">Write the code for your web role</span></span>
<span data-ttu-id="0e66e-187">在本節中，您將建立應用程式顯示的各個頁面。</span><span class="sxs-lookup"><span data-stu-id="0e66e-187">In this section, you create the various pages that your application displays.</span></span>

1. <span data-ttu-id="0e66e-188">在 Visual Studio 的 OnlineOrder.cs 檔案中，將現有的命名空間定義取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="0e66e-188">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="0e66e-189">在 [方案總管] 中，按兩下 [Controllers\HomeController.cs]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="0e66e-190">在檔案頂端新增下列 **using** 陳述式，以納入您剛建立之模型的命名空間，以及服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="0e66e-190">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="0e66e-191">同時在 Visual Studio 的 HomeController.cs 檔案中，也將現有的命名空間定義取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="0e66e-191">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span> <span data-ttu-id="0e66e-192">此程式碼包含將項目提交給佇列的處理方法。</span><span class="sxs-lookup"><span data-stu-id="0e66e-192">This code contains methods for handling the submission of items to the queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect to Submit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for the submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from the submission
           // form.
           [HttpPost]
           // Attribute to help prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting to queue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="0e66e-193">從 [建置] 功能表中，按一下 [建置方案] 來測試您的工作到目前為止是否正確無誤。</span><span class="sxs-lookup"><span data-stu-id="0e66e-193">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span></span>
5. <span data-ttu-id="0e66e-194">現在，為先前建立的 `Submit()` 方法建立檢視。</span><span class="sxs-lookup"><span data-stu-id="0e66e-194">Now, create the view for the `Submit()` method you created earlier.</span></span> <span data-ttu-id="0e66e-195">在 `Submit()` 方法 (未採用任何參數的 `Submit()` 的多載) 內按一下滑鼠右鍵，然後選擇 [新增檢視]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-195">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="0e66e-196">隨即出現對話方塊，供您建立檢視。</span><span class="sxs-lookup"><span data-stu-id="0e66e-196">A dialog box appears for creating the view.</span></span> <span data-ttu-id="0e66e-197">在 [範本] 清單中，選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-197">In the **Template** list, choose **Create**.</span></span> <span data-ttu-id="0e66e-198">在 [模型類別] 清單中，按一下 [OnlineOrder] 類別。</span><span class="sxs-lookup"><span data-stu-id="0e66e-198">In the **Model class** list, click the **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="0e66e-199">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="0e66e-199">Click **Add**.</span></span>
8. <span data-ttu-id="0e66e-200">現在，變更應用程式的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="0e66e-200">Now, change the displayed name of your application.</span></span> <span data-ttu-id="0e66e-201">在 [方案總管] 中，按兩下 **Views\Shared\\_Layout.cshtml** 檔案以在 Visual Studio 編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="0e66e-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="0e66e-202">將所有出現的 **My ASP.NET Application** 取代為 **LITWARE'S Products**。</span><span class="sxs-lookup"><span data-stu-id="0e66e-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="0e66e-203">移除 [首頁]、[關於] 和 [連絡人] 連結。</span><span class="sxs-lookup"><span data-stu-id="0e66e-203">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="0e66e-204">刪除反白顯示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="0e66e-204">Delete the highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="0e66e-205">最後，修改提交頁面，以納入佇列的一些相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0e66e-205">Finally, modify the submission page to include some information about the queue.</span></span> <span data-ttu-id="0e66e-206">在 [方案總管] 中，按兩下 [Views\Home\Submit.cshtml] 檔案以在 Visual Studio 編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="0e66e-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="0e66e-207">在 `<h2>Submit</h2>` 後面新增下列一行。</span><span class="sxs-lookup"><span data-stu-id="0e66e-207">Add the following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="0e66e-208">目前 `ViewBag.MessageCount` 是空的。</span><span class="sxs-lookup"><span data-stu-id="0e66e-208">For now, the `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="0e66e-209">稍後您將在其中填入資料。</span><span class="sxs-lookup"><span data-stu-id="0e66e-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting to be processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="0e66e-210">您現在已實作 UI。</span><span class="sxs-lookup"><span data-stu-id="0e66e-210">You now have implemented your UI.</span></span> <span data-ttu-id="0e66e-211">您可以按 **F5** 執行應用程式，確認它的外觀與預期一樣。</span><span class="sxs-lookup"><span data-stu-id="0e66e-211">You can press **F5** to run your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-the-code-for-submitting-items-to-a-service-bus-queue"></a><span data-ttu-id="0e66e-212">撰寫增程式碼以提交項目給服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="0e66e-212">Write the code for submitting items to a Service Bus queue</span></span>
<span data-ttu-id="0e66e-213">現在，將新增程式碼以提交項目給佇列。</span><span class="sxs-lookup"><span data-stu-id="0e66e-213">Now, add code for submitting items to a queue.</span></span> <span data-ttu-id="0e66e-214">首先，您會建立一個類別，並使其包含服務匯流排佇列連接資訊。</span><span class="sxs-lookup"><span data-stu-id="0e66e-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="0e66e-215">接著，從 Global.aspx.cs 初始化您的連線。</span><span class="sxs-lookup"><span data-stu-id="0e66e-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="0e66e-216">最後，更新稍早在 HomeController.cs 建立的提交程式碼，以將項目實際提交給服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="0e66e-216">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span></span>

1. <span data-ttu-id="0e66e-217">在 [方案總管] 中，於 [FrontendWebRole] 上按一下滑鼠右鍵 (在專案而非角色上按一下滑鼠右鍵)。</span><span class="sxs-lookup"><span data-stu-id="0e66e-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span></span> <span data-ttu-id="0e66e-218">按一下 [新增]，然後按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="0e66e-219">將類別命名為 **QueueConnector.cs**。</span><span class="sxs-lookup"><span data-stu-id="0e66e-219">Name the class **QueueConnector.cs**.</span></span> <span data-ttu-id="0e66e-220">按一下 [新增] 以建立類別。</span><span class="sxs-lookup"><span data-stu-id="0e66e-220">Click **Add** to create the class.</span></span>
3. <span data-ttu-id="0e66e-221">現在，新增可封裝連線資訊、並初始化與服務匯流排佇列連線的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0e66e-221">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span></span> <span data-ttu-id="0e66e-222">以下列程式碼取代 QueueConnector.cs 的整個內容，並將值輸入 `your Service Bus namespace` (命名空間名稱) 和 `yourKey`，後者是先前取自 Azure 入口網站的**主要金鑰**。</span><span class="sxs-lookup"><span data-stu-id="0e66e-222">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from the portal.
           public const string Namespace = "your Service Bus namespace";
   
           // The name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create the namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http to be friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create the namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create the queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client to the queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="0e66e-223">現在，請確定會呼叫您的 **Initialize** 方法。</span><span class="sxs-lookup"><span data-stu-id="0e66e-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="0e66e-224">在 [方案總管] 中，按兩下 [Global.asax\Global.asax.cs]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="0e66e-225">在 **Application_Start** 方法的結尾新增下列程式碼行。</span><span class="sxs-lookup"><span data-stu-id="0e66e-225">Add the following line of code at the end of the **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="0e66e-226">最後，更新稍早建立的 Web 程式碼，以提交項目給佇列。</span><span class="sxs-lookup"><span data-stu-id="0e66e-226">Finally, update the web code you created earlier, to submit items to the queue.</span></span> <span data-ttu-id="0e66e-227">在 [方案總管] 中，按兩下 [Controllers\HomeController.cs]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="0e66e-228">如下所示更新 `Submit()` 方法 (未採用任何參數的多載)，以取得佇列的訊息計數。</span><span class="sxs-lookup"><span data-stu-id="0e66e-228">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you to perform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get the queue, and obtain the message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="0e66e-229">如下所示更新 `Submit(OnlineOrder order)` 方法 (採用一個參數的多載)，以提交訂單資訊給佇列。</span><span class="sxs-lookup"><span data-stu-id="0e66e-229">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from the order.
           var message = new BrokeredMessage(order);
   
           // Submit the order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="0e66e-230">現在您可以重新執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e66e-230">You can now run the application again.</span></span> <span data-ttu-id="0e66e-231">每次您一提交訂單，訊息計數便會增加。</span><span class="sxs-lookup"><span data-stu-id="0e66e-231">Each time you submit an order, the message count increases.</span></span>
   
   ![][18]

## <a name="create-the-worker-role"></a><span data-ttu-id="0e66e-232">建立背景工作角色</span><span class="sxs-lookup"><span data-stu-id="0e66e-232">Create the worker role</span></span>
<span data-ttu-id="0e66e-233">您現在將建立背景工作角色來處理所提交的訂單。</span><span class="sxs-lookup"><span data-stu-id="0e66e-233">You will now create the worker role that processes the order submissions.</span></span> <span data-ttu-id="0e66e-234">本範例使用 **Worker Role with Service Bus Queue** Visual Studio 專案範本。</span><span class="sxs-lookup"><span data-stu-id="0e66e-234">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="0e66e-235">您已經從入口網站取得必要的認證。</span><span class="sxs-lookup"><span data-stu-id="0e66e-235">You already obtained the required credentials from the portal.</span></span>

1. <span data-ttu-id="0e66e-236">請確定您已將 Visual Studio 連接到您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e66e-236">Make sure you have connected Visual Studio to your Azure account.</span></span>
2. <span data-ttu-id="0e66e-237">在 Visual Studio 的 [方案總管] 中，於 [MultiTierApp] 專案下的 [角色] 資料夾上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="0e66e-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span></span>
3. <span data-ttu-id="0e66e-238">按一下 [新增]，然後按一下 [新的背景工作角色專案]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="0e66e-239">[新增新的角色專案] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0e66e-239">The **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="0e66e-240">在 [新增新的角色專案] 對話方塊中，按一下 [具有服務匯流排佇列的背景工作角色]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-240">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="0e66e-241">在 [名稱] 方塊中，將專案命名為 **OrderProcessingRole**。</span><span class="sxs-lookup"><span data-stu-id="0e66e-241">In the **Name** box, name the project **OrderProcessingRole**.</span></span> <span data-ttu-id="0e66e-242">然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-242">Then click **Add**.</span></span>
6. <span data-ttu-id="0e66e-243">將您在＜建立服務匯流排命名空間＞一節的步驟 9 中取得的連接字串複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="0e66e-243">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span></span>
7. <span data-ttu-id="0e66e-244">在 [方案總管] 中，請以滑鼠右鍵按一下您在步驟 5 中所建立的 **OrderProcessingRole** (請確定您是在 [角色] 下而不是類別下的 **OrderProcessingRole** 按一下滑鼠右鍵)。</span><span class="sxs-lookup"><span data-stu-id="0e66e-244">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span></span> <span data-ttu-id="0e66e-245">然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="0e66e-246">在 [屬性] 對話方塊的 [設定] 索引標籤中，按一下 **Microsoft.ServiceBus.ConnectionString** 的 [值] 方塊內部，然後貼上您在步驟 6 中複製的端點值。</span><span class="sxs-lookup"><span data-stu-id="0e66e-246">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="0e66e-247">建立 **OnlineOrder**，以代表您從佇列處理它們時的順序。</span><span class="sxs-lookup"><span data-stu-id="0e66e-247">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span></span> <span data-ttu-id="0e66e-248">您可以重複使用已建立的類別。</span><span class="sxs-lookup"><span data-stu-id="0e66e-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="0e66e-249">在 [方案總管] 中，以滑鼠右鍵按一下 **OrderProcessingRole** 類別 (在類別圖示而不是角色上按一下滑鼠右鍵)。</span><span class="sxs-lookup"><span data-stu-id="0e66e-249">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span></span> <span data-ttu-id="0e66e-250">按一下 [新增]，然後按一下 [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="0e66e-251">瀏覽至 **FrontendWebRole\Models** 的子資料夾，並按兩下 [OnlineOrder.cs]，以將其新增至此專案。</span><span class="sxs-lookup"><span data-stu-id="0e66e-251">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span></span>
11. <span data-ttu-id="0e66e-252">在 **WorkerRole.cs** 中，將 **QueueName** 變數值從 `"ProcessingQueue"` 變更為 `"OrdersQueue"`，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="0e66e-252">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span></span>
    
    ```csharp
    // The name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="0e66e-253">在 WorkerRole.cs 檔案頂端新增下列 using 陳述式。</span><span class="sxs-lookup"><span data-stu-id="0e66e-253">Add the following using statement at the top of the WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="0e66e-254">在 `Run()` 函式的 `OnMessage()` 呼叫內，以下列程式碼取代 `try` 子句的內容。</span><span class="sxs-lookup"><span data-stu-id="0e66e-254">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View the message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="0e66e-255">您已完成應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e66e-255">You have completed the application.</span></span> <span data-ttu-id="0e66e-256">您可以測試完整的應用程式，方法是以滑鼠右鍵按一下 [方案總管] 中的 MultiTierApp 專案、選取 [設定為啟始專案]，然後按下 F5。</span><span class="sxs-lookup"><span data-stu-id="0e66e-256">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="0e66e-257">請注意，訊息計數不會增加，因為背景工作角色會處理佇列中的項目，並將它們標示為完成。</span><span class="sxs-lookup"><span data-stu-id="0e66e-257">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span></span> <span data-ttu-id="0e66e-258">您可以檢視 Azure 計算模擬器 UI，來查看背景工作角色的追蹤輸出。</span><span class="sxs-lookup"><span data-stu-id="0e66e-258">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span></span> <span data-ttu-id="0e66e-259">作法為在工作列的通知區中的計算模擬器圖示上按一下滑鼠右鍵，並選取 [顯示計算模擬器 UI]。</span><span class="sxs-lookup"><span data-stu-id="0e66e-259">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="0e66e-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e66e-260">Next steps</span></span>
<span data-ttu-id="0e66e-261">若要深入了解服務匯流排，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="0e66e-261">To learn more about Service Bus, see the following resources:</span></span>  

* <span data-ttu-id="0e66e-262">[Azure 服務匯流排文件][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="0e66e-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="0e66e-263">[服務匯流排服務頁面][sbacom]</span><span class="sxs-lookup"><span data-stu-id="0e66e-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="0e66e-264">[如何使用服務匯流排佇列][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="0e66e-264">[How to Use Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="0e66e-265">若要深入了解多層式案例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="0e66e-265">To learn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="0e66e-266">[使用儲存體資料表、佇列與 Blob 的 .NET 多層式應用程式][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="0e66e-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
