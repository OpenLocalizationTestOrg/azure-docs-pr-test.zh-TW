---
title: "Azure 無伺服器概觀 | Microsoft Docs"
description: "在雲端建立功能強大的解決方案，而不必考慮基礎結構。"
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 6803e22a78e27c15ff4fec301cd5bdd55aacd3e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a><span data-ttu-id="388e4-103">Azure 無伺服器搭配 Functions 和 Logic Apps 的概觀</span><span class="sxs-lookup"><span data-stu-id="388e4-103">Overview of Azure Serverless with Functions and Logic Apps</span></span>

<span data-ttu-id="388e4-104">無伺服器應用程式提供的好處包括加速開發、減少必要的程式碼，以及簡單調整。</span><span class="sxs-lookup"><span data-stu-id="388e4-104">Serverless applications offer benefits of an increase in speed of development, reduction in required code, and simplicity with scale.</span></span>  <span data-ttu-id="388e4-105">本文描述無伺服器解決方案的各種屬性和 Azure 無伺服器供應項目。</span><span class="sxs-lookup"><span data-stu-id="388e4-105">This article goes into the different attributes of serverless solutions, and Azure serverless offerings.</span></span>

## <a name="what-is-serverless"></a><span data-ttu-id="388e4-106">什麼是無伺服器？</span><span class="sxs-lookup"><span data-stu-id="388e4-106">What is serverless?</span></span>

<span data-ttu-id="388e4-107">無伺服器並不表示沒有伺服器 - 只是表示開發人員不需要擔心伺服器。</span><span class="sxs-lookup"><span data-stu-id="388e4-107">Serverless doesn't mean there are no servers - it just means the developer doesn't have to worry about servers.</span></span>  <span data-ttu-id="388e4-108">大部分的傳統應用程式開發主要是回答有關調整、裝載及監視解決方案的問題，以滿足應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="388e4-108">A large part of traditional application development is answering questions around scaling, hosting, and monitoring solutions to meet the demands of the application.</span></span>  <span data-ttu-id="388e4-109">在無伺服器中，這些問題由解決方案本身來處理。</span><span class="sxs-lookup"><span data-stu-id="388e4-109">With Serverless, these questions are taken care of as part of the solution.</span></span>  <span data-ttu-id="388e4-110">此外，無伺服器應用程式是以耗用量為基礎的方案計費。</span><span class="sxs-lookup"><span data-stu-id="388e4-110">In addition, Serverless applications are billed on a consumption-based plan.</span></span>  <span data-ttu-id="388e4-111">如果從未使用過應用程式，則永遠不會產生費用。</span><span class="sxs-lookup"><span data-stu-id="388e4-111">If the application is never used, a charge is never incurred.</span></span>  <span data-ttu-id="388e4-112">這些功能可讓開發人員專注於解決方案的商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="388e4-112">These features allow developers to focus solely on the business logic of the solution.</span></span>

<span data-ttu-id="388e4-113">Azure 中有關非伺服器的核心服務是 [Azure Functions](https://azure.microsoft.com/services/functions/) 和 [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)。</span><span class="sxs-lookup"><span data-stu-id="388e4-113">The core services in Azure around Serverless are [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>  <span data-ttu-id="388e4-114">這兩種解決方案遵循上述原則，可讓開發人員以最少程式碼建置健全的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="388e4-114">Both of these solutions follow the principles above, and allow developers to build robust cloud applications with minimal code.</span></span>

## <a name="what-are-azure-functions"></a><span data-ttu-id="388e4-115">什麼是 Azure Functions？</span><span class="sxs-lookup"><span data-stu-id="388e4-115">What are Azure Functions?</span></span>

<span data-ttu-id="388e4-116">Azure Functions 是可在雲端輕鬆執行程式碼片段或「函數」的解決方案。</span><span class="sxs-lookup"><span data-stu-id="388e4-116">Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="388e4-117">您可以只撰寫處理手邊問題所需的程式碼，而不需擔心要執行它的整個應用程式或基礎結構。</span><span class="sxs-lookup"><span data-stu-id="388e4-117">You can write just the code you need for the problem at hand, without worrying about a whole application or the infrastructure to run it.</span></span> <span data-ttu-id="388e4-118">Functions 可讓開發更有生產力，而且您可以使用您選擇的開發語言，例如 C#、F#、Node.js、Python 或 PHP。</span><span class="sxs-lookup"><span data-stu-id="388e4-118">Functions can make development even more productive, and you can use your development language of choice, such as C#, F#, Node.js, Python, or PHP.</span></span> <span data-ttu-id="388e4-119">只需依程式碼執行的時間多寡付費，Azure 會視需要而調整。</span><span class="sxs-lookup"><span data-stu-id="388e4-119">Pay only for the time your code runs and Azure scales as needed.</span></span>

<span data-ttu-id="388e4-120">如果您想要直接進入正題並開始使用 Azure Functions，請從 [建立您的第一個Azure Functions](../azure-functions/functions-create-first-azure-function.md)著手。</span><span class="sxs-lookup"><span data-stu-id="388e4-120">If you want to jump right in and get started with Azure Functions, start with [Create your first Azure Function](../azure-functions/functions-create-first-azure-function.md).</span></span> <span data-ttu-id="388e4-121">如果您要尋找更多有關 Functions 的技術資訊，請參閱 [開發人員參考](../azure-functions/functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="388e4-121">If you are looking for more technical information about Functions, see the [developer reference](../azure-functions/functions-reference.md).</span></span>

## <a name="what-are-azure-logic-apps"></a><span data-ttu-id="388e4-122">什麼是 Azure Logic Apps？</span><span class="sxs-lookup"><span data-stu-id="388e4-122">What are Azure Logic Apps?</span></span>

<span data-ttu-id="388e4-123">Azure Logic Apps 能夠在雲端中簡化和實作可調整的整合和工作流程。</span><span class="sxs-lookup"><span data-stu-id="388e4-123">Azure Logic Apps provides a way to simplify and implement scalable integrations and workflows in the cloud.</span></span> <span data-ttu-id="388e4-124">它提供視覺化設計工具，以一系列的步驟 (稱為工作流程) 為您的程序建立模型並加以自動化。</span><span class="sxs-lookup"><span data-stu-id="388e4-124">It provides a visual designer to model and automate your process as a series of steps called a workflow.</span></span>  <span data-ttu-id="388e4-125">雲端和內部部署服務中有[許多連接器](../connectors/apis-list.md)，可快速將無伺服器應用程式連線至其他 API。</span><span class="sxs-lookup"><span data-stu-id="388e4-125">There are [many connectors](../connectors/apis-list.md) across cloud and on-premises services to quickly connect a serverless app to other APIs.</span></span>  <span data-ttu-id="388e4-126">邏輯應用程式是以觸發程序為開端 (如「當帳戶加入至 Dynamics CRM 時」)，而在觸發後可以開始處理各種組合的動作、轉換和條件邏輯。</span><span class="sxs-lookup"><span data-stu-id="388e4-126">A logic app begins with a trigger (like 'When an account is added to Dynamics CRM') and after firing can begin many combinations actions, conversions, and condition logic.</span></span>  <span data-ttu-id="388e4-127">在一個程序中協調不同的 Azure Functions 時，Logic Apps 是絕佳選擇 - 尤其是當程序需要與外部系統或 API 互動時。</span><span class="sxs-lookup"><span data-stu-id="388e4-127">Logic Apps is a great choice when orchestrating different Azure Functions in a process - especially when the process requires interacting with an external system or API.</span></span>

<span data-ttu-id="388e4-128">若要開始使用 Logic Apps，請從[建立您的第一個邏輯應用程式](logic-apps-create-a-logic-app.md)開始。</span><span class="sxs-lookup"><span data-stu-id="388e4-128">To get started with Logic Apps, start with [creating your first logic app](logic-apps-create-a-logic-app.md).</span></span>  <span data-ttu-id="388e4-129">如果您要尋找更多有關 Logic Apps 的技術資訊，請參閱[開發人員參考](logic-apps-workflow-actions-triggers.md)。</span><span class="sxs-lookup"><span data-stu-id="388e4-129">If you are looking for more technical information about Logic Apps, see the [developer reference](logic-apps-workflow-actions-triggers.md).</span></span>

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a><span data-ttu-id="388e4-130">如何在 Azure 中建置和部署無伺服器應用程式？</span><span class="sxs-lookup"><span data-stu-id="388e4-130">How can I build and deploy Serverless applications in Azure?</span></span>

<span data-ttu-id="388e4-131">Azure 提供一組豐富的工具，涵蓋開發、部署和管理無伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="388e4-131">Azure provides a rich set of tools across development, deployment, and management of Serverless apps.</span></span>  <span data-ttu-id="388e4-132">您可以直接在 Azure 入口網站中建置應用程式，或使用 [Visual Studio 中的工具](logic-apps-serverless-get-started-vs.md)來建置。</span><span class="sxs-lookup"><span data-stu-id="388e4-132">Apps can be built directly in the Azure portal, or with [tooling from Visual Studio](logic-apps-serverless-get-started-vs.md).</span></span>  <span data-ttu-id="388e4-133">開發應用程式之後，就可以[立即部署](logic-apps-create-deploy-template.md)。</span><span class="sxs-lookup"><span data-stu-id="388e4-133">Once an application has been developed it can be [deployed instantly](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="388e4-134">Azure 也支援監視無伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="388e4-134">Azure also provides monitoring for serverless apps.</span></span>  <span data-ttu-id="388e4-135">您可以從 Azure 入口網站、透過 API 或 SDK，或使用 OMS 和 Application Insights 的整合式工具，存取此監視功能。</span><span class="sxs-lookup"><span data-stu-id="388e4-135">This monitoring can be accessed from the Azure portal, through the API or SDKs, or with integrated tooling to OMS and Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="388e4-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="388e4-136">Next steps</span></span>

* [<span data-ttu-id="388e4-137">開始在 Visual Studio 中建置無伺服器應用程式</span><span class="sxs-lookup"><span data-stu-id="388e4-137">Get started building a Serverless app in Visual Studio</span></span>](logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="388e4-138">使用無伺服器建立 Customer Insights 儀表板</span><span class="sxs-lookup"><span data-stu-id="388e4-138">Create a customer insights dashboard with Serverless</span></span>](logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="388e4-139">建置邏輯應用程式的部署範本</span><span class="sxs-lookup"><span data-stu-id="388e4-139">Build a deployment template for a logic app</span></span>](logic-apps-create-deploy-template.md)