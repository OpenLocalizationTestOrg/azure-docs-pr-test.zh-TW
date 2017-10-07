---
title: "aaaExamples & 常見案例-Azure 邏輯應用程式 |Microsoft 文件"
description: "透過範例、案例和教學課程深入了解 Logic Apps"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a><span data-ttu-id="26609-103">Azure Logic Apps 的範例和常見案例</span><span class="sxs-lookup"><span data-stu-id="26609-103">Examples and common scenarios for Azure Logic Apps</span></span>

<span data-ttu-id="26609-104">您深入了解 toohelp hello 許多模式和 Azure 邏輯應用程式中的功能，以下是常見的範例和案例。</span><span class="sxs-lookup"><span data-stu-id="26609-104">toohelp you learn more about hello many patterns and capabilities in Azure Logic Apps, here are common examples and scenarios.</span></span>

## <a name="key-scenarios-for-logic-apps"></a><span data-ttu-id="26609-105">邏輯應用程式的重要案例</span><span class="sxs-lookup"><span data-stu-id="26609-105">Key scenarios for logic apps</span></span>

<span data-ttu-id="26609-106">Azure Logic Apps 針對不同的服務提供了彈性的協調流程和整合功能。</span><span class="sxs-lookup"><span data-stu-id="26609-106">Azure Logic Apps provides resilient orchestration and integration for different services.</span></span> <span data-ttu-id="26609-107">hello 邏輯應用程式服務是 「 無伺服器 」，讓您沒有小數位數或執行個體的相關 tooworry-所有您具有 toodo 定義 hello 工作流程 （觸發程序和動作）。</span><span class="sxs-lookup"><span data-stu-id="26609-107">hello Logic Apps service is "serverless", so you don't have tooworry about scale or instances - all you have toodo is define hello workflow (trigger and actions).</span></span> <span data-ttu-id="26609-108">小數位數、 可用性和效能，則會處理 hello 基礎平台。</span><span class="sxs-lookup"><span data-stu-id="26609-108">hello underlying platform handles scale, availability, and performance.</span></span> <span data-ttu-id="26609-109">在任何案例中，您需要 toocoordinate 多個動作，尤其是跨多個系統，是很大的使用案例，Azure 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26609-109">Any scenario where you need toocoordinate multiple actions, especially across multiple systems, is a great use case for Azure Logic Apps.</span></span> <span data-ttu-id="26609-110">以下有一些模式和範例。</span><span class="sxs-lookup"><span data-stu-id="26609-110">Here are some patterns and examples.</span></span>

## <a name="respond-tootriggers-and-extend-actions"></a><span data-ttu-id="26609-111">回應 tootriggers 和擴充動作</span><span class="sxs-lookup"><span data-stu-id="26609-111">Respond tootriggers and extend actions</span></span>

<span data-ttu-id="26609-112">每個邏輯應用程式都會從觸發程序來開始。</span><span class="sxs-lookup"><span data-stu-id="26609-112">Every logic app begins with a trigger.</span></span> <span data-ttu-id="26609-113">例如，您的工作流程可以從開始排程事件，手動叫用或從外部系統中，事件這類 hello 」 時將檔案加入 tooan FTP 伺服器 」 的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="26609-113">For example, your workflow can start with a schedule event, a manual invocation, or an event from an external system, such as hello "when a file is added tooan FTP server" trigger.</span></span> <span data-ttu-id="26609-114">Azure 邏輯應用程式目前支援超過 100 個的已備妥要使用連接器，從內部部署 SAP tooMicrosoft 認知的服務。</span><span class="sxs-lookup"><span data-stu-id="26609-114">Azure Logic Apps currently supports over 100 ready-to-use connectors, ranging from on-premises SAP tooMicrosoft Cognitive Services.</span></span> <span data-ttu-id="26609-115">對於可能沒有已發佈連接器的系統和服務，您也可以延伸邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26609-115">For systems and services that might not have published connectors, you can also extend logic apps.</span></span>

* [<span data-ttu-id="26609-116">建立自訂觸發程序或動作</span><span class="sxs-lookup"><span data-stu-id="26609-116">Create custom triggers or actions</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="26609-117">為工作流程執行設定長時間執行的動作</span><span class="sxs-lookup"><span data-stu-id="26609-117">Set up long-running actions for workflow runs</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="26609-118">回應 tooexternal 事件和動作與 webhook</span><span class="sxs-lookup"><span data-stu-id="26609-118">Respond tooexternal events and actions with webhooks</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="26609-119">呼叫時，觸發程序，或巢狀處理同步回應 tooHTTP 要求的工作流程</span><span class="sxs-lookup"><span data-stu-id="26609-119">Call, trigger, or nest workflows with synchronous responses tooHTTP requests</span></span>](../logic-apps/logic-apps-http-endpoint.md)
* [<span data-ttu-id="26609-120">教學課程： 回應 tooTwilio SMS webhook 和傳送回應的文字</span><span class="sxs-lookup"><span data-stu-id="26609-120">Tutorial: Respond tooTwilio SMS webhooks and send a text response</span></span>](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [<span data-ttu-id="26609-121">教學課程︰使用 Logic Apps 和 Power BI 在幾分鐘內建置具有 AI 技術的社交儀表板</span><span class="sxs-lookup"><span data-stu-id="26609-121">Tutorial: Build an AI-powered social dashboard in minutes with Logic Apps and Power BI</span></span>](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a><span data-ttu-id="26609-122">錯誤處理、記錄和控制流程功能</span><span class="sxs-lookup"><span data-stu-id="26609-122">Error handling, logging, and control flow capabilities</span></span>

<span data-ttu-id="26609-123">邏輯應用程式包含豐富的功能，可用於處理進階控制流程，例如條件、開關、迴圈和範圍。</span><span class="sxs-lookup"><span data-stu-id="26609-123">Logic apps include rich capabilities for advanced control flow, like conditions, switches, loops, and scopes.</span></span> <span data-ttu-id="26609-124">tooensure 復原方案，您也可以實作錯誤和例外狀況處理在工作流程中。</span><span class="sxs-lookup"><span data-stu-id="26609-124">tooensure resilient solutions, you can also implement error and exception handling in your workflows.</span></span> <span data-ttu-id="26609-125">針對工作流程執行狀態的通知和診斷記錄，Azure Logic Apps 也提供了監視和警示。</span><span class="sxs-lookup"><span data-stu-id="26609-125">For notification and diagnostic logs for workflow run status, Azure Logic Apps also provides monitoring and alerts.</span></span>

* [<span data-ttu-id="26609-126">使用 switch 陳述式來執行不同動作</span><span class="sxs-lookup"><span data-stu-id="26609-126">Perform different actions with switch statements</span></span>](../logic-apps/logic-apps-switch-case.md)
* [<span data-ttu-id="26609-127">在邏輯應用程式中使用迴圈和批次處理陣列和集合中的項目</span><span class="sxs-lookup"><span data-stu-id="26609-127">Process items in arrays and collections with loops and batches in logic apps</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="26609-128">在工作流程中撰寫錯誤和例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="26609-128">Author error and exception handling in a workflow</span></span>](../logic-apps/logic-apps-exception-handling.md)
* [<span data-ttu-id="26609-129">開啟現有 Logic Apps 的監視、記錄和警示</span><span class="sxs-lookup"><span data-stu-id="26609-129">Turn on monitoring, logging, and alerts for existing logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="26609-130">建立 Logic Apps 時開啟監視和診斷記錄</span><span class="sxs-lookup"><span data-stu-id="26609-130">Turn on monitoring and diagnostics logging when creating logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [<span data-ttu-id="26609-131">使用案例︰醫療保健公司如何使用邏輯應用程式的例外狀況處理來處理 HL7 FHIR 工作流程</span><span class="sxs-lookup"><span data-stu-id="26609-131">Use case: How a healthcare company uses logic app exception handling for HL7 FHIR workflows</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a><span data-ttu-id="26609-132">部署和管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="26609-132">Deploy and manage logic apps</span></span>

<span data-ttu-id="26609-133">您可以完全透過 Visual Studio、Visual Studio Team Services 或其他任何原始檔控制和自動化建置工具，來開發及部署邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26609-133">You can fully develop and deploy logic apps with Visual Studio, Visual Studio Team Services, or any other source control and automated build tools.</span></span> <span data-ttu-id="26609-134">toosupport 及部署的工作流程相依資源範本中的連線，邏輯應用程式使用 Azure 資源部署範本。</span><span class="sxs-lookup"><span data-stu-id="26609-134">toosupport deployment for workflows and dependent connections in a resource template, logic apps use Azure resource deployment templates.</span></span> <span data-ttu-id="26609-135">Visual Studio 工具自動產生這些範本，您可以簽入版本控制的 toosource 控制項。</span><span class="sxs-lookup"><span data-stu-id="26609-135">Visual Studio tools automatically generate these templates, which you can check in toosource control for versioning.</span></span>

* [<span data-ttu-id="26609-136">建立自動部署範本</span><span class="sxs-lookup"><span data-stu-id="26609-136">Create an automated deployment template</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="26609-137">在 Visual Studio 中建置和部署 Logic Apps</span><span class="sxs-lookup"><span data-stu-id="26609-137">Build and deploy logic apps from Visual Studio</span></span>](../logic-apps/logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="26609-138">監視您的 logic apps hello 健全狀況</span><span class="sxs-lookup"><span data-stu-id="26609-138">Monitor hello health of your logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a><span data-ttu-id="26609-139">執行內的內容類型、轉換 (Conversion) 及轉換 (Transformation)</span><span class="sxs-lookup"><span data-stu-id="26609-139">Content types, conversions, and transformations within a run</span></span>

<span data-ttu-id="26609-140">您可以存取、 轉換，並使用 hello hello Azure 邏輯應用程式中的許多函數轉換多個內容類型[工作流程定義語言](http://aka.ms/logicappsdocs)。</span><span class="sxs-lookup"><span data-stu-id="26609-140">You can access, convert, and transform multiple content types by using hello many functions in hello Azure Logic Apps [workflow definition language](http://aka.ms/logicappsdocs).</span></span> <span data-ttu-id="26609-141">例如，您可以將轉換的字串、 JSON 和 XML 之間以 hello`@json()`和`@xml()`工作流程運算式。</span><span class="sxs-lookup"><span data-stu-id="26609-141">For example, you can convert between a string, JSON, and XML with hello `@json()` and `@xml()` workflow expressions.</span></span> <span data-ttu-id="26609-142">hello Logic Apps 引擎服務之間的不失真方式保留內容類型 toosupport 內容傳輸。</span><span class="sxs-lookup"><span data-stu-id="26609-142">hello Logic Apps engine preserves content types toosupport content transfer in a lossless manner between services.</span></span>

* <span data-ttu-id="26609-143">[處理非 JSON 內容類型](../logic-apps/logic-apps-content-type.md)，例如 `application/xml`、`application/octet-stream` 和 `multipart/formdata`</span><span class="sxs-lookup"><span data-stu-id="26609-143">[Handle non-JSON content types](../logic-apps/logic-apps-content-type.md), like `application/xml`, `application/octet-stream`, and `multipart/formdata`</span></span>
* [<span data-ttu-id="26609-144">工作流程運算式在邏輯應用程式中的運作方式</span><span class="sxs-lookup"><span data-stu-id="26609-144">How workflow expressions work in logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="26609-145">參考：Azure Logic Apps 工作流程定義語言</span><span class="sxs-lookup"><span data-stu-id="26609-145">Reference: Azure Logic Apps workflow definition language</span></span>](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a><span data-ttu-id="26609-146">其他整合和功能</span><span class="sxs-lookup"><span data-stu-id="26609-146">Other integrations and capabilities</span></span>

<span data-ttu-id="26609-147">邏輯應用程式也提供與許多服務 (例如 Azure Functions、Azure API 管理、Azure App Service) 和自訂 HTTP 端點 (例如 REST 和 SOAP) 的整合。</span><span class="sxs-lookup"><span data-stu-id="26609-147">Logic apps also offer integration with many services, like Azure Functions, Azure API Management, Azure App Services, and custom HTTP endpoints, for example, REST and SOAP.</span></span>

* [<span data-ttu-id="26609-148">使用 Azure 無伺服器建立即時社交儀表板</span><span class="sxs-lookup"><span data-stu-id="26609-148">Create a real-time social dashboard with Azure Serverless</span></span>](../logic-apps/logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="26609-149">從邏輯應用程式呼叫 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="26609-149">Call Azure Functions from logic apps</span></span>](../logic-apps/logic-apps-azure-functions.md)
* [<span data-ttu-id="26609-150">案例：使用 Azure Functions 觸發邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="26609-150">Scenario: Trigger logic apps with Azure Functions</span></span>](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [<span data-ttu-id="26609-151">部落格︰從邏輯應用程式呼叫 SOAP 端點</span><span class="sxs-lookup"><span data-stu-id="26609-151">Blog: Call SOAP endpoints from logic apps</span></span>](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a><span data-ttu-id="26609-152">端對端案例</span><span class="sxs-lookup"><span data-stu-id="26609-152">End-to-end scenarios</span></span>

* [<span data-ttu-id="26609-153">白皮書：使用 Azure 服務 (例如 Logic Apps) 進行企業整合端對端案例管理</span><span class="sxs-lookup"><span data-stu-id="26609-153">Whitepaper: Enterprise integration end-to-end case management with Azure services, like Logic Apps</span></span>](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a><span data-ttu-id="26609-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26609-154">Next steps</span></span>

- [<span data-ttu-id="26609-155">處理邏輯應用程式中的錯誤和例外狀況</span><span class="sxs-lookup"><span data-stu-id="26609-155">Handle errors and exceptions in logic apps</span></span>](../logic-apps/logic-apps-exception-handling.md)
- [<span data-ttu-id="26609-156">撰寫工作流程定義與 hello 工作流程定義語言</span><span class="sxs-lookup"><span data-stu-id="26609-156">Author workflow definitions with hello workflow definition language</span></span>](../logic-apps/logic-apps-author-definitions.md)
- [<span data-ttu-id="26609-157">提交有關我們該如何改善 Azure Logic Apps 的評論、問題、意見或建議</span><span class="sxs-lookup"><span data-stu-id="26609-157">Submit your comments, questions, feedback, or suggestions for how can we improve Azure Logic Apps</span></span>](https://feedback.azure.com/forums/287593-logic-apps)