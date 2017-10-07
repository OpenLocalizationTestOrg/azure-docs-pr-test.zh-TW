---
title: "使用 Azure 服務匯流排 aaa.NET 多層式應用程式 |Microsoft 文件"
description: ".NET 教學課程，可協助您開發使用服務匯流排佇列 toocommunicate 各層之間的 Azure 中的多層式應用程式。"
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
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="17e6f-103">使用 Azure 服務匯流排佇列的 .NET 多層應用程式</span><span class="sxs-lookup"><span data-stu-id="17e6f-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="17e6f-104">簡介</span><span class="sxs-lookup"><span data-stu-id="17e6f-104">Introduction</span></span>
<span data-ttu-id="17e6f-105">開發 Microsoft Azure 很容易使用 Visual Studio 和 hello 免費 Azure SDK for.NET。</span><span class="sxs-lookup"><span data-stu-id="17e6f-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="17e6f-106">本教學課程中引導您完成 hello 步驟 toocreate 使用多個在本機環境中執行的 Azure 資源的應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="17e6f-107">您將學習下列 hello:</span><span class="sxs-lookup"><span data-stu-id="17e6f-107">You will learn hello following:</span></span>

* <span data-ttu-id="17e6f-108">如何 tooenable 進行 Azure 開發以單一電腦下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="17e6f-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="17e6f-109">如何將 Visual Studio toodevelop toouse azure。</span><span class="sxs-lookup"><span data-stu-id="17e6f-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="17e6f-110">如何 toocreate 使用 web 和背景工作角色在 Azure 中的多層式應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="17e6f-111">如何使用服務匯流排佇列的 toocommunicate 之間層。</span><span class="sxs-lookup"><span data-stu-id="17e6f-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="17e6f-112">在本教學課程中，您會建置並執行 Azure 雲端服務中的 hello 多層式應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="17e6f-113">hello 前端是 ASP.NET MVC web 角色，且 hello 後端會使用服務匯流排佇列背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="17e6f-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="17e6f-114">您可以建立 hello 相同多層式的應用程式與 hello 前端的 web 專案，部署的 tooan Azure 的網站，而不是雲端服務。</span><span class="sxs-lookup"><span data-stu-id="17e6f-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="17e6f-115">您也可以試用 hello [.NET 在內部部署/雲端的混合式應用程式](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="17e6f-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="17e6f-116">hello 下列螢幕擷取畫面顯示 hello 完成應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="17e6f-117">案例概觀：內部角色通訊</span><span class="sxs-lookup"><span data-stu-id="17e6f-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="17e6f-118">toosubmit 處理 hello 前端 UI 元件，在 hello web 角色中，執行的順序必須與 hello 中間層邏輯 hello 背景工作角色執行互動。</span><span class="sxs-lookup"><span data-stu-id="17e6f-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="17e6f-119">這個範例會使用服務匯流排訊息 hello hello 各層之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="17e6f-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="17e6f-120">使用服務匯流排傳訊 hello web 和中介層之間可分隔的兩個元件。</span><span class="sxs-lookup"><span data-stu-id="17e6f-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="17e6f-121">相較之下 toodirect 訊息 （也就是 TCP 或 HTTP） hello web 層未直接; 連接 toohello 中介層而是它推入工作單位，做為訊息，到 Service Bus 可靠地保留它們，直到準備好 tooconsume hello 中介層並進行處理。</span><span class="sxs-lookup"><span data-stu-id="17e6f-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="17e6f-122">服務匯流排提供兩個實體 toosupport 代理傳訊： 佇列和主題。</span><span class="sxs-lookup"><span data-stu-id="17e6f-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="17e6f-123">每個訊息佇列，傳送 toohello 佇列由單一接收者。</span><span class="sxs-lookup"><span data-stu-id="17e6f-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="17e6f-124">主題也支援每個發佈的訊息可提供 tooa 註冊 hello 主題的訂用帳戶中的 hello 發行/訂閱的模式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="17e6f-125">每個訂閱在邏輯上會維護自己的訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="17e6f-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="17e6f-126">訂閱也可以設定限制 hello 集到的訊息傳遞 hello 訂閱佇列 toothose 符合 hello 篩選條件的篩選規則。</span><span class="sxs-lookup"><span data-stu-id="17e6f-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="17e6f-127">hello 下列範例會使用服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="17e6f-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="17e6f-128">此通訊機制具有數個超越直接傳訊的優點：</span><span class="sxs-lookup"><span data-stu-id="17e6f-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="17e6f-129">**暫時分離。**</span><span class="sxs-lookup"><span data-stu-id="17e6f-129">**Temporal decoupling.**</span></span> <span data-ttu-id="17e6f-130">與 hello 非同步訊息模式中，產生者和消費者不需要在 hello 線上相同的時間。</span><span class="sxs-lookup"><span data-stu-id="17e6f-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="17e6f-131">服務匯流排可靠地儲存訊息，直到 hello 取用方準備要接收訊息。</span><span class="sxs-lookup"><span data-stu-id="17e6f-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="17e6f-132">這可讓 hello hello 分散式應用程式 toobe 中斷連接，可能是主動，例如，為了進行維護，或因為 tooa 元件損毀，而不會影響整體系統元件。</span><span class="sxs-lookup"><span data-stu-id="17e6f-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="17e6f-133">此外，hello 取用應用程式可能只需要線上 toocome hello 一天的特定時間。</span><span class="sxs-lookup"><span data-stu-id="17e6f-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="17e6f-134">**負載調節。**</span><span class="sxs-lookup"><span data-stu-id="17e6f-134">**Load leveling.**</span></span> <span data-ttu-id="17e6f-135">在許多應用程式，系統負載會隨著時間改變時所需的每個工作單位的 hello 處理時間通常不變。</span><span class="sxs-lookup"><span data-stu-id="17e6f-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="17e6f-136">調解訊息產生者和消費者與佇列表示取用應用程式 （hello 背景工作） 只需要 toobe 該 hello 佈建 tooaccommodate 平均負載，而非尖峰負載。</span><span class="sxs-lookup"><span data-stu-id="17e6f-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="17e6f-137">hello 深度 hello 佇列成長，且合約會隨著 hello 連入負載而改變。</span><span class="sxs-lookup"><span data-stu-id="17e6f-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="17e6f-138">這可直接節省金錢根據提供的基礎結構需要的 tooservice hello 應用程式負載 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="17e6f-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="17e6f-139">**負載平衡。**</span><span class="sxs-lookup"><span data-stu-id="17e6f-139">**Load balancing.**</span></span> <span data-ttu-id="17e6f-140">隨著負載增加，多個背景工作處理序可以加入 tooread hello 佇列中。</span><span class="sxs-lookup"><span data-stu-id="17e6f-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="17e6f-141">只有其中一個 hello 背景工作處理序處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="17e6f-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="17e6f-142">此外，此提取為基礎的負載平衡可讓最有效地利用 hello 工作者機器即使背景工作電腦各有不同，根據處理能力，因為它們會在他們自己的最大速率提取訊息。</span><span class="sxs-lookup"><span data-stu-id="17e6f-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="17e6f-143">此模式通常稱為 hello*競爭取用者*模式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="17e6f-144">hello 下列各節討論 hello 實作程式碼，此架構。</span><span class="sxs-lookup"><span data-stu-id="17e6f-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="17e6f-145">設定 hello 開發環境</span><span class="sxs-lookup"><span data-stu-id="17e6f-145">Set up hello development environment</span></span>
<span data-ttu-id="17e6f-146">您可以開始開發 Azure 應用程式之前，取得 hello 工具，並設定您的開發環境。</span><span class="sxs-lookup"><span data-stu-id="17e6f-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="17e6f-147">安裝 hello Azure SDK for.NET，從 hello SDK[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="17e6f-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="17e6f-148">在 hello **.NET**資料行中，按一下 hello 版本[Visual Studio](http://www.visualstudio.com)您使用。</span><span class="sxs-lookup"><span data-stu-id="17e6f-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="17e6f-149">hello 步驟在此教學課程使用 Visual Studio 2015，但也可使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="17e6f-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="17e6f-150">當系統提示 toorun 或儲存 hello 安裝程式時，按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="17e6f-151">在 hello **Web Platform Installer**，按一下 **安裝**並繼續進行 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="17e6f-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="17e6f-152">Hello 安裝完成之後，您將會擁有一切所需的 toostart toodevelop hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="17e6f-153">hello SDK 包含工具，讓您輕鬆地開發 Visual Studio 中的 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="17e6f-154">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="17e6f-154">Create a namespace</span></span>
<span data-ttu-id="17e6f-155">hello 下一個步驟是 toocreate 服務命名空間，和取得共用存取簽章 (SAS) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="17e6f-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="17e6f-156">命名空間會為每個透過服務匯流排公開的應用程式提供應用程式界限。</span><span class="sxs-lookup"><span data-stu-id="17e6f-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="17e6f-157">建立命名空間時，會產生 hello 系統 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="17e6f-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="17e6f-158">命名空間和 SAS 金鑰的 hello 組合提供服務匯流排 tooauthenticate 存取 tooan 應用程式的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="17e6f-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="17e6f-159">建立 Web 角色</span><span class="sxs-lookup"><span data-stu-id="17e6f-159">Create a web role</span></span>
<span data-ttu-id="17e6f-160">在本節中，建立 hello 前端應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="17e6f-161">首先，您會建立您的應用程式會顯示 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="17e6f-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="17e6f-162">在這之後，加入程式碼送出項目 tooa Service Bus 佇列，並顯示 hello 佇列的相關狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="17e6f-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="17e6f-163">建立 hello 專案</span><span class="sxs-lookup"><span data-stu-id="17e6f-163">Create hello project</span></span>
1. <span data-ttu-id="17e6f-164">使用系統管理員權限，請啟動 Visual Studio： 以滑鼠右鍵按一下 hello **Visual Studio**程式圖示，然後按一下**系統管理員身分執行**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="17e6f-165">hello Azure 計算模擬器中，將在本文中，稍後討論需要 Visual Studio 會使用系統管理員權限來啟動。</span><span class="sxs-lookup"><span data-stu-id="17e6f-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="17e6f-166">在 Visual Studio 中的 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="17e6f-167">從 已安裝的範本 的 Visual C# 下，按一下 雲端，然後按一下Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="17e6f-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="17e6f-168">名稱 hello 專案**MultiTierApp**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="17e6f-169">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="17e6f-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="17e6f-170">從 **.NET Framework 4.5** 角色中，按兩下 [ASP.NET Web 角色]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="17e6f-171">將滑鼠停留在**WebRole1**下**Azure 雲端服務方案**、 按一下 hello 鉛筆圖示，和 hello web 角色重新命名過**FrontendWebRole**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="17e6f-172">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="17e6f-172">Then click **OK**.</span></span> <span data-ttu-id="17e6f-173">(請確定您輸入 "Frontend"，其中 e 為小寫，而不是 "FrontEnd"。)</span><span class="sxs-lookup"><span data-stu-id="17e6f-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="17e6f-174">從 hello**新增 ASP.NET 專案**對話方塊中的，在 hello**選取範本**清單中，按一下**MVC**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="17e6f-175">仍在 hello**新增 ASP.NET 專案**對話方塊方塊中，按一下 hello**變更驗證** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="17e6f-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="17e6f-176">在 hello**變更驗證**對話方塊中，按一下**非驗證**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="17e6f-177">在本教學課程中，您會部署不需要使用者登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="17e6f-178">在 hello**新增 ASP.NET 專案**對話方塊中，按一下 **確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="17e6f-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="17e6f-179">在**方案總管] 中**，在 hello **FrontendWebRole**專案中，以滑鼠右鍵按一下**參考**，然後按一下 [**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="17e6f-180">按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="17e6f-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="17e6f-181">選取 hello **WindowsAzure.ServiceBus**封裝中，按一下 **安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="17e6f-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="17e6f-182">請注意該 hello 需要用戶端組件現在會參考與已新增一些新的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="17e6f-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="17e6f-183">在 [方案總管] 中，於 [模型] 上按一下滑鼠右鍵、按一下 [新增]，再按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="17e6f-184">在 [hello**名稱**] 方塊中，輸入 hello 名稱**OnlineOrder.cs**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="17e6f-185">然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="17e6f-186">撰寫您的 web 角色的 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="17e6f-186">Write hello code for your web role</span></span>
<span data-ttu-id="17e6f-187">在本節中，您建立 hello 會顯示您的應用程式的各個頁面。</span><span class="sxs-lookup"><span data-stu-id="17e6f-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="17e6f-188">在 Visual Studio 中的 hello OnlineOrder.cs 檔案，取代現有的命名空間定義以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="17e6f-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
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
2. <span data-ttu-id="17e6f-189">在 [方案總管] 中，按兩下 [Controllers\HomeController.cs]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="17e6f-190">新增下列 hello**使用**在 hello hello 最上方的陳述式檔案適用於您剛剛建立，以及服務匯流排的模型 tooinclude hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="17e6f-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="17e6f-191">也在 Visual Studio 中的 hello HomeController.cs 檔案，取代現有的命名空間定義 hello 下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="17e6f-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="17e6f-192">這個程式碼包含的方法來處理 hello 送出的項目 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="17e6f-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
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
4. <span data-ttu-id="17e6f-193">從 hello**建置**功能表上，按一下 **建置方案**tootest hello 精確度的工作為止。</span><span class="sxs-lookup"><span data-stu-id="17e6f-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="17e6f-194">現在，建立 hello hello 檢視`Submit()`您稍早建立的方法。</span><span class="sxs-lookup"><span data-stu-id="17e6f-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="17e6f-195">Hello 內以滑鼠右鍵按一下`Submit()`方法 (hello 多載`Submit()`，不接受任何參數)，然後選擇 **加入檢視**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="17e6f-196">建立 hello 檢視會出現的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="17e6f-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="17e6f-197">在 hello**範本**清單中，選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="17e6f-198">在 hello**模型類別**清單中，按一下 hello **OnlineOrder**類別。</span><span class="sxs-lookup"><span data-stu-id="17e6f-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="17e6f-199">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="17e6f-199">Click **Add**.</span></span>
8. <span data-ttu-id="17e6f-200">現在，變更 hello 顯示應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="17e6f-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="17e6f-201">在**方案總管 中**，連按兩下**_layout.cshtml\\_Layout.cshtml**檔案 tooopen hello Visual Studio 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="17e6f-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="17e6f-202">將所有出現的 **My ASP.NET Application** 取代為 **LITWARE'S Products**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="17e6f-203">移除 hello**首頁**，**有關**，和**連絡人**連結。</span><span class="sxs-lookup"><span data-stu-id="17e6f-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="17e6f-204">刪除 hello 反白顯示程式碼：</span><span class="sxs-lookup"><span data-stu-id="17e6f-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="17e6f-205">最後，修改 hello 送出頁面 tooinclude 某些 hello 佇列的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="17e6f-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="17e6f-206">在**方案總管 中**，連按兩下**Views\Home\Submit.cshtml**檔案 tooopen hello Visual Studio 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="17e6f-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="17e6f-207">新增下列一行之後 hello `<h2>Submit</h2>`。</span><span class="sxs-lookup"><span data-stu-id="17e6f-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="17e6f-208">現在，hello`ViewBag.MessageCount`是空的。</span><span class="sxs-lookup"><span data-stu-id="17e6f-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="17e6f-209">稍後您將在其中填入資料。</span><span class="sxs-lookup"><span data-stu-id="17e6f-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="17e6f-210">您現在已實作 UI。</span><span class="sxs-lookup"><span data-stu-id="17e6f-210">You now have implemented your UI.</span></span> <span data-ttu-id="17e6f-211">您可以按**F5** toorun 您的應用程式，並確認它看起來正常。</span><span class="sxs-lookup"><span data-stu-id="17e6f-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="17e6f-212">撰寫 hello 送出項目 tooa 服務匯流排佇列的程式碼</span><span class="sxs-lookup"><span data-stu-id="17e6f-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="17e6f-213">現在，加入送出項目 tooa 佇列的程式碼。</span><span class="sxs-lookup"><span data-stu-id="17e6f-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="17e6f-214">首先，您會建立一個類別，並使其包含服務匯流排佇列連接資訊。</span><span class="sxs-lookup"><span data-stu-id="17e6f-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="17e6f-215">接著，從 Global.aspx.cs 初始化您的連線。</span><span class="sxs-lookup"><span data-stu-id="17e6f-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="17e6f-216">最後，更新您建立稍早在 HomeController.cs tooactually 送出項目 tooa 服務匯流排佇列中的 hello 提交程式碼。</span><span class="sxs-lookup"><span data-stu-id="17e6f-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="17e6f-217">在**方案總管 中**，以滑鼠右鍵按一下**FrontendWebRole** （以滑鼠右鍵按一下 hello 專案，不 hello 角色）。</span><span class="sxs-lookup"><span data-stu-id="17e6f-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="17e6f-218">按一下 新增，然後按一下類別。</span><span class="sxs-lookup"><span data-stu-id="17e6f-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="17e6f-219">Hello 類別命名**QueueConnector.cs**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="17e6f-220">按一下**新增**toocreate hello 類別。</span><span class="sxs-lookup"><span data-stu-id="17e6f-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="17e6f-221">現在，加入程式碼，用以封裝 hello 連接資訊和初始化 hello 連線 tooa 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="17e6f-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="17e6f-222">Hello，下列程式碼中，以取代 QueueConnector.cs hello 整個內容，並輸入值`your Service Bus namespace`（命名空間名稱） 和`yourKey`，也就是 hello**主索引鍵**您先前取得的 hello Azure入口網站。</span><span class="sxs-lookup"><span data-stu-id="17e6f-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
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
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="17e6f-223">現在，請確定會呼叫您的 **Initialize** 方法。</span><span class="sxs-lookup"><span data-stu-id="17e6f-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="17e6f-224">在 [方案總管] 中，按兩下 [Global.asax\Global.asax.cs]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="17e6f-225">新增下列一行程式碼結尾 hello hello hello **Application_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="17e6f-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="17e6f-226">最後，更新 hello 送出項目 toohello 佇列稍早建立的 web 程式碼。</span><span class="sxs-lookup"><span data-stu-id="17e6f-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="17e6f-227">在 [方案總管] 中，按兩下 [Controllers\HomeController.cs]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="17e6f-228">更新 hello`Submit()`方法 （hello 多載會採用任何參數），如下所示 tooget hello 訊息計數 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="17e6f-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="17e6f-229">更新 hello`Submit(OnlineOrder order)`方法 （hello 多載會接受一個參數），如下所示 toosubmit 排序資訊 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="17e6f-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="17e6f-230">您現在可以執行一次 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-230">You can now run hello application again.</span></span> <span data-ttu-id="17e6f-231">每次提交訂單時，會增加 hello 訊息計數。</span><span class="sxs-lookup"><span data-stu-id="17e6f-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="17e6f-232">建立 hello 背景工作角色</span><span class="sxs-lookup"><span data-stu-id="17e6f-232">Create hello worker role</span></span>
<span data-ttu-id="17e6f-233">您即將建立 hello 處理 hello 順序送出的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="17e6f-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="17e6f-234">這個範例會使用 hello**具有服務匯流排佇列背景工作角色**Visual Studio 專案範本。</span><span class="sxs-lookup"><span data-stu-id="17e6f-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="17e6f-235">您已向 hello 入口網站取得 hello 所需的認證。</span><span class="sxs-lookup"><span data-stu-id="17e6f-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="17e6f-236">請確定您已經連接 Visual Studio tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="17e6f-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="17e6f-237">在 Visual Studio 中**方案總管 中**以滑鼠右鍵按一下**角色**下 hello 資料夾**MultiTierApp**專案。</span><span class="sxs-lookup"><span data-stu-id="17e6f-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="17e6f-238">按一下 新增，然後按一下新的背景工作角色專案。</span><span class="sxs-lookup"><span data-stu-id="17e6f-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="17e6f-239">hello**加入新的角色專案** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="17e6f-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="17e6f-240">在 hello**加入新的角色專案**對話方塊中，按一下 **具有服務匯流排佇列背景工作角色**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="17e6f-241">在 hello**名稱**方塊中，名稱 hello 專案**OrderProcessingRole**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="17e6f-242">然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-242">Then click **Add**.</span></span>
6. <span data-ttu-id="17e6f-243">您在步驟 9 的 hello 「 建立服務匯流排命名空間 」 一節 toohello 剪貼簿中取得複製 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="17e6f-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="17e6f-244">在**方案總管 中**，以滑鼠右鍵按一下 hello **OrderProcessingRole**您在步驟 5 中建立 (請確定您按一下滑鼠右鍵**OrderProcessingRole**下**角色**，和不 hello 類別)。</span><span class="sxs-lookup"><span data-stu-id="17e6f-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="17e6f-245">然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="17e6f-246">在 [hello**設定**hello] 索引標籤**屬性**對話方塊中，按一下 hello 的內部**值**方塊**microsoft.servicebus.connectionstring 所指定**，然後貼上您在步驟 6 中複製的 hello 端點值。</span><span class="sxs-lookup"><span data-stu-id="17e6f-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="17e6f-247">建立**OnlineOrder**類別 toorepresent hello 訂單，為您從 hello 佇列處理它們。</span><span class="sxs-lookup"><span data-stu-id="17e6f-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="17e6f-248">您可以重複使用已建立的類別。</span><span class="sxs-lookup"><span data-stu-id="17e6f-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="17e6f-249">在**方案總管 中**，以滑鼠右鍵按一下 hello **OrderProcessingRole**類別 （以滑鼠右鍵按一下 hello 類別圖示，不 hello 角色）。</span><span class="sxs-lookup"><span data-stu-id="17e6f-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="17e6f-250">按一下 [新增]，然後按一下 [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="17e6f-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="17e6f-251">瀏覽 toohello 子資料夾**FrontendWebRole\Models**，然後按兩下**OnlineOrder.cs** tooadd 它 toothis 專案。</span><span class="sxs-lookup"><span data-stu-id="17e6f-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="17e6f-252">在**WorkerRole.cs**，變更 hello hello 值**QueueName**變數從`"ProcessingQueue"`太`"OrdersQueue"`hello 下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="17e6f-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="17e6f-253">新增 hello 下列 using 陳述式在 hello hello WorkerRole.cs 檔案最上方。</span><span class="sxs-lookup"><span data-stu-id="17e6f-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="17e6f-254">在 hello`Run()`函式，在 hello`OnMessage()`呼叫，取代 hello hello 內容`try`以下列程式碼的 hello 子句。</span><span class="sxs-lookup"><span data-stu-id="17e6f-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="17e6f-255">您已完成 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e6f-255">You have completed hello application.</span></span> <span data-ttu-id="17e6f-256">您可以測試 hello 完整的應用程式，以滑鼠右鍵按一下方案總管 中的 hello MultiTierApp 專案選取**設定為啟始專案**，然後按 F5。</span><span class="sxs-lookup"><span data-stu-id="17e6f-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="17e6f-257">請注意，訊息計數不會遞增，因為 hello 背景工作角色處理 hello 佇列中的項目，並將其標示為完成。</span><span class="sxs-lookup"><span data-stu-id="17e6f-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="17e6f-258">您可以藉由檢視 hello Azure 計算模擬器 UI 中看到 hello 追蹤輸出的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="17e6f-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="17e6f-259">您可以在 hello 工作列的通知區域中的 hello 模擬器圖示上按一下滑鼠右鍵，然後選取**顯示計算模擬器 UI**。</span><span class="sxs-lookup"><span data-stu-id="17e6f-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="17e6f-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17e6f-260">Next steps</span></span>
<span data-ttu-id="17e6f-261">toolearn 有關 Service Bus 的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="17e6f-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="17e6f-262">[Azure 服務匯流排文件][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="17e6f-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="17e6f-263">[服務匯流排服務頁面][sbacom]</span><span class="sxs-lookup"><span data-stu-id="17e6f-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="17e6f-264">[如何 tooUse Service Bus 佇列][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="17e6f-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="17e6f-265">toolearn 有關多層式案例的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="17e6f-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="17e6f-266">[使用儲存體資料表、佇列與 Blob 的 .NET 多層式應用程式][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="17e6f-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

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
