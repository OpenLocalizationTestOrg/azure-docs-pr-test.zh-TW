---
title: "使用工作流程來連接應用程式和整合資料 - Azure Logic Apps | Microsoft Docs"
description: "使用 Azure Logic Apps 來連接應用程式和整合資料，以建立工作流程並自動化程序。"
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 64af585f81d39daaa5373d7cf080404ee5f1b037
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-are-logic-apps"></a><span data-ttu-id="21e09-103">什麼是 Logic Apps？</span><span class="sxs-lookup"><span data-stu-id="21e09-103">What are Logic Apps?</span></span>
<span data-ttu-id="21e09-104">Logic Apps 提供簡化和實作雲端中可擴充整合和工作流程的途徑。</span><span class="sxs-lookup"><span data-stu-id="21e09-104">Logic Apps provide a way to simplify and implement scalable integrations and workflows in the cloud.</span></span> <span data-ttu-id="21e09-105">它提供視覺化設計工具，以一系列的步驟 (也稱為工作流程) 為您的程序建立模型並加以自動化。</span><span class="sxs-lookup"><span data-stu-id="21e09-105">It provides a visual designer to model and automate your process as a series of steps known as a workflow.</span></span>  <span data-ttu-id="21e09-106">雲端和內部部署中有 [許多連接器](../connectors/apis-list.md) 可快速整合各項服務和通訊協定。</span><span class="sxs-lookup"><span data-stu-id="21e09-106">There are [many connectors](../connectors/apis-list.md) across the cloud and on-premises to quickly integrate across services and protocols.</span></span>  <span data-ttu-id="21e09-107">邏輯應用程式是以觸發程序為開端 (如「當帳戶新增至 Dynamics CRM 時」)，而在觸發後可以開始處理各種組合的動作、轉換和條件邏輯。</span><span class="sxs-lookup"><span data-stu-id="21e09-107">A logic app begins with a trigger (like 'When an account is added to Dynamics CRM') and after firing can begin many combinations of actions, conversions, and condition logic.</span></span>

<span data-ttu-id="21e09-108">使用 Logic Apps 的優點包括︰</span><span class="sxs-lookup"><span data-stu-id="21e09-108">The advantages of using Logic Apps include the following:</span></span>  

* <span data-ttu-id="21e09-109">使用易於了解的設計工具來設計複雜程序以節省時間</span><span class="sxs-lookup"><span data-stu-id="21e09-109">Saving time by designing complex processes using easy to understand design tools</span></span>
* <span data-ttu-id="21e09-110">順暢地實作難以在程式碼中實作的模式和工作流程。</span><span class="sxs-lookup"><span data-stu-id="21e09-110">Implementing patterns and workflows seamlessly, that would otherwise be difficult to implement in code</span></span>
* <span data-ttu-id="21e09-111">從範本快速開始使用</span><span class="sxs-lookup"><span data-stu-id="21e09-111">Getting started quickly from templates</span></span>
* <span data-ttu-id="21e09-112">使用自己的自訂 API、程式碼和動作來自訂邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="21e09-112">Customizing your logic app with your own custom APIs, code, and actions</span></span>
* <span data-ttu-id="21e09-113">連接並同步處理跨內部部署與雲端的不同系統</span><span class="sxs-lookup"><span data-stu-id="21e09-113">Connect and synchronise disparate systems across on-premises and the cloud</span></span>
* <span data-ttu-id="21e09-114">利用頂級整合支援打造 BizTalk Server、API 管理、Azure Functions 和 Azure 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="21e09-114">Build off of BizTalk server, API Management, Azure Functions, and Azure Service Bus with first-class integration support</span></span>

<span data-ttu-id="21e09-115">Logic Apps 是完全受管理的 iPaaS (整合平台即服務)，可讓開發人員不必擔心建置裝載、延展性、可用性和管理。</span><span class="sxs-lookup"><span data-stu-id="21e09-115">Logic Apps is a fully managed iPaaS (integration Platform as a Service) allowing developers not to have to worry about building hosting, scalability, availability and management.</span></span>  <span data-ttu-id="21e09-116">邏輯應用程式會自動相應增加以滿足需求。</span><span class="sxs-lookup"><span data-stu-id="21e09-116">Logic Apps will scale up automatically to meet demand.</span></span>

![流程應用程式設計工具](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

<span data-ttu-id="21e09-118">如先前所述，您可以使用 Logic Apps 將商務程序自動化。</span><span class="sxs-lookup"><span data-stu-id="21e09-118">As mentioned, with Logic Apps, you can automate business processes.</span></span> <span data-ttu-id="21e09-119">以下是一些範例︰</span><span class="sxs-lookup"><span data-stu-id="21e09-119">Here are a couple examples:</span></span>  

* <span data-ttu-id="21e09-120">將上傳至 FTP 伺服器的檔案移到 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="21e09-120">Move files uploaded to an FTP server into Azure Storage</span></span>
* <span data-ttu-id="21e09-121">處理並路由傳送跨內部部署與雲端系統的訂單</span><span class="sxs-lookup"><span data-stu-id="21e09-121">Process and route orders across on-premises and cloud systems</span></span>
* <span data-ttu-id="21e09-122">監視有關特定主題的所有推文、分析情感，以及針對需要後續追蹤的項目建立警示和工作。</span><span class="sxs-lookup"><span data-stu-id="21e09-122">Monitor all tweets about a certain topic, analyze the sentiment, and create alerts and tasks for items needing followup.</span></span>

<span data-ttu-id="21e09-123">這些案例都能從視覺化設計工具加以設定，無需撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="21e09-123">Scenarios such as these can be configured all from the visual designer and without writing a single line of code.</span></span> <span data-ttu-id="21e09-124">[立即開始建置邏輯應用程式][create]。</span><span class="sxs-lookup"><span data-stu-id="21e09-124">Get started [building your logic app now][create].</span></span>  <span data-ttu-id="21e09-125">撰寫後 - 邏輯應用程式可能會 [快速部署並重新設定](../logic-apps/logic-apps-create-deploy-template.md) 於多個環境和區域。</span><span class="sxs-lookup"><span data-stu-id="21e09-125">Once written - a logic app can be [quickly deployed and reconfigured](../logic-apps/logic-apps-create-deploy-template.md) across multiple environments and regions.</span></span>

## <a name="why-logic-apps"></a><span data-ttu-id="21e09-126">為什麼要使用 Logic Apps？</span><span class="sxs-lookup"><span data-stu-id="21e09-126">Why Logic Apps?</span></span>
<span data-ttu-id="21e09-127">Logic Apps 可提高企業整合的速度和延展性。</span><span class="sxs-lookup"><span data-stu-id="21e09-127">Logic Apps brings speed and scalability into the enterprise integration space.</span></span>  <span data-ttu-id="21e09-128">容易使用的設計工具、各種可用的觸發程序和動作以及強大的管理工具，均讓您的 API 集中管理比以往更簡單。</span><span class="sxs-lookup"><span data-stu-id="21e09-128">The ease of use of the designer, variety of available triggers and actions, and powerful management tools make centralizing your APIs simpler than ever.</span></span>  <span data-ttu-id="21e09-129">隨著企業邁向數位化，Logic Apps 可讓您將舊版和最先進的系統連接在一起。</span><span class="sxs-lookup"><span data-stu-id="21e09-129">As businesses move towards digitalization, Logic Apps allows you to connect legacy and cutting-edge systems together.</span></span>

<span data-ttu-id="21e09-130">此外，透過我們的[企業整合帳戶][biztalk]，您可以利用 [XML 訊息][xml]、[交易夥伴管理][tpm]等的功能，擴展至成熟的整合案例。</span><span class="sxs-lookup"><span data-stu-id="21e09-130">Additionally, with our [Enterprise Integration Account][biztalk] you can scale to mature integration scenarios with the power of a [XML messaging][xml], [trading partner management][tpm], and more.</span></span>

* <span data-ttu-id="21e09-131">**容易使用的設計工具** - Logic Apps 可在瀏覽器中或使用 Visual Studio 工具端對端地設計。</span><span class="sxs-lookup"><span data-stu-id="21e09-131">**Easy to use design tools** - Logic Apps can be designed end-to-end in the browser or with Visual Studio tools.</span></span> <span data-ttu-id="21e09-132">從觸發程序著手 - 從簡單的排程，以至建立 GitHub 問題時。</span><span class="sxs-lookup"><span data-stu-id="21e09-132">Start with a trigger - from a simple schedule to when a GitHub issue is created.</span></span> <span data-ttu-id="21e09-133">然後，使用豐富的連接器資源庫協調任何數量的動作。</span><span class="sxs-lookup"><span data-stu-id="21e09-133">Then orchestrate any number of actions using the rich gallery of connectors.</span></span>
* <span data-ttu-id="21e09-134">**輕鬆連接 API** - 即使可輕鬆說明的撰寫工作，也很難在程式碼中實作。</span><span class="sxs-lookup"><span data-stu-id="21e09-134">**Connect APIs easily** - Even composition tasks that are easy to describe are difficult to implement in code.</span></span> <span data-ttu-id="21e09-135">Logic Apps 可讓您輕鬆連接不同的系統。</span><span class="sxs-lookup"><span data-stu-id="21e09-135">Logic Apps makes it easy to connect disparate systems.</span></span> <span data-ttu-id="21e09-136">想要將您的雲端行銷解決方案連接到內部部署計費系統嗎？</span><span class="sxs-lookup"><span data-stu-id="21e09-136">Want to connect your cloud marketing solution to your on-premises billing system?</span></span> <span data-ttu-id="21e09-137">想要利用企業服務匯流排集中處理跨 API 與系統的訊息嗎？</span><span class="sxs-lookup"><span data-stu-id="21e09-137">Want to centralize messaging across APIs and systems with an Enterprise Service Bus?</span></span> <span data-ttu-id="21e09-138">邏輯應用程式可用最快、最可靠方式，提供這些問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="21e09-138">Logic apps are the fastest, most reliable way to deliver solutions to these problems.</span></span>
* <span data-ttu-id="21e09-139">**從範本快速開始使用** - 為了協助您開始使用，我們提供[範本庫][templates]，讓您快速建立一些常用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="21e09-139">**Get started quickly from templates** - To help you get started we've provided a [gallery of templates][templates] that allow you to rapidly create some common solutions.</span></span> <span data-ttu-id="21e09-140">從進階 B2B 解決方案到簡單的 SaaS 連線 (甚至只為了「好玩」) - 資源庫是開始使用Logic Apps 強大功能的最快方式。</span><span class="sxs-lookup"><span data-stu-id="21e09-140">From advanced B2B solutions to simple SaaS connectivity, and even a few that are just 'for fun' - the gallery is the fastest way to get started with the power of Logic Apps.</span></span>
* <span data-ttu-id="21e09-141">**現成可用的擴充性** - 找不到您所需要的連接器嗎？</span><span class="sxs-lookup"><span data-stu-id="21e09-141">**Extensibility baked-in** - Don't see the connector you need?</span></span> <span data-ttu-id="21e09-142">Logic Apps 主要是用來處理您自己的 API 和程式碼。您可以輕鬆地建立自己的 API 應用程式以做為自訂連接器，或呼叫 [Azure 函式](https://functions.azure.com)以執行隨選程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="21e09-142">Logic Apps is designed to work with your own APIs and code; you can easily create your own API app to use as a custom connector, or call into an [Azure Function](https://functions.azure.com) to execute snippets of code on-demand.</span></span> 
* <span data-ttu-id="21e09-143">**真正的整合能力** - 入門容易，並且可依需求擴充。</span><span class="sxs-lookup"><span data-stu-id="21e09-143">**Real integration horsepower** - Start easy and grow as you need.</span></span> <span data-ttu-id="21e09-144">Logic Apps 可輕易地讓 Microsoft 領先業界的整合解決方案 BizTalk 發揮效益，使整合專業人員得以建置其所需的解決方案。</span><span class="sxs-lookup"><span data-stu-id="21e09-144">Logic Apps can easily leverage the power of BizTalk, Microsoft's industry leading integration solution to enable integration professionals to build the solutions they need.</span></span> <span data-ttu-id="21e09-145">深入了解[企業整合套件](../logic-apps/logic-apps-enterprise-integration-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="21e09-145">Find out more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="logic-app-concepts"></a><span data-ttu-id="21e09-146">邏輯應用程式概念</span><span class="sxs-lookup"><span data-stu-id="21e09-146">Logic App Concepts</span></span>
<span data-ttu-id="21e09-147">以下是構成 Logic Apps 使用性的一些重要元素。</span><span class="sxs-lookup"><span data-stu-id="21e09-147">The following are some of the key pieces that comprise the Logic Apps experience.</span></span> 

* <span data-ttu-id="21e09-148">**工作流程** - Logic Apps 提供圖形化的方式，以一系列的步驟或工作流程的形式為您的商務程序建立模型。</span><span class="sxs-lookup"><span data-stu-id="21e09-148">**Workflow** - Logic Apps provides a graphical way to model your business processes as a series of steps or a workflow.</span></span>
* <span data-ttu-id="21e09-149">**受管理連接器** - 邏輯應用程式需要存取資料和服務。</span><span class="sxs-lookup"><span data-stu-id="21e09-149">**Managed Connectors** - Your logic apps need access to data and services.</span></span> <span data-ttu-id="21e09-150">受管理連接器是為了讓協助您連接及使用資料而特別設計的。</span><span class="sxs-lookup"><span data-stu-id="21e09-150">Managed connectors are created specifically to aid you when you are connecting to and working with your data.</span></span> <span data-ttu-id="21e09-151">請參閱[受管理連接器][managedapis]中目前可用的連接器清單。</span><span class="sxs-lookup"><span data-stu-id="21e09-151">See the list of connectors available now in [managed connectors][managedapis].</span></span>
* <span data-ttu-id="21e09-152">**觸發程序** - 某些受管理連接器也可以做為觸發程序。</span><span class="sxs-lookup"><span data-stu-id="21e09-152">**Triggers** - Some Managed Connectors can also act as a trigger.</span></span> <span data-ttu-id="21e09-153">觸發程序會根據特定的事件建立新的工作流程執行個體，例如在電子郵件送達或您的 Azure 儲存體帳戶有所變更時。</span><span class="sxs-lookup"><span data-stu-id="21e09-153">A trigger starts a new instance of a workflow based on a specific event, like the arrival of an e-mail or a change in your Azure Storage account.</span></span>
* <span data-ttu-id="21e09-154">**動作** - 工作流程中觸發程序後的每個步驟登稱為動作。</span><span class="sxs-lookup"><span data-stu-id="21e09-154">**Actions** - Each step after the trigger in a workflow is called an action.</span></span> <span data-ttu-id="21e09-155">每個動作通常會對應至受管理連接器或自訂 API 應用程式上的作業。</span><span class="sxs-lookup"><span data-stu-id="21e09-155">Each action typically maps to an operation on your managed connector or custom API apps.</span></span>
* <span data-ttu-id="21e09-156">**企業整合套件** - 在更進階的整合案例中，Logic Apps 會包含來自 BizTalk 的功能。</span><span class="sxs-lookup"><span data-stu-id="21e09-156">**Enterprise Integration Pack** - For more advanced integration scenarios, Logic Apps includes capabilities from BizTalk.</span></span> <span data-ttu-id="21e09-157">BizTalk 是 Microsoft 領先業界的整合平台。</span><span class="sxs-lookup"><span data-stu-id="21e09-157">BizTalk is Microsoft's industry leading integration platform.</span></span> <span data-ttu-id="21e09-158">「企業整合套件」連接器可讓您輕鬆地將驗證、轉換等項目納入邏輯應用程式工作流程中。</span><span class="sxs-lookup"><span data-stu-id="21e09-158">The Enterprise Integration Pack connectors allow you to easily include validation, transformation, and more in to your Logic App workflows.</span></span>

## <a name="getting-started"></a><span data-ttu-id="21e09-159">開始使用</span><span class="sxs-lookup"><span data-stu-id="21e09-159">Getting Started</span></span>
* <span data-ttu-id="21e09-160">若要開始使用 Logic Apps，請遵循[建立 Logic Apps][create] 教學課程。</span><span class="sxs-lookup"><span data-stu-id="21e09-160">To get started with Logic Apps, follow the [create a Logic App][create] tutorial.</span></span>  
* [<span data-ttu-id="21e09-161">檢視常見的範例和案例</span><span class="sxs-lookup"><span data-stu-id="21e09-161">View common examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="21e09-162">您可以使用 Logic Apps 自動化商務程序</span><span class="sxs-lookup"><span data-stu-id="21e09-162">You can automate business processes with Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694) 
* [<span data-ttu-id="21e09-163">了解如何整合您的系統與 Logic Apps</span><span class="sxs-lookup"><span data-stu-id="21e09-163">Learn How to Integrate your systems with Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
