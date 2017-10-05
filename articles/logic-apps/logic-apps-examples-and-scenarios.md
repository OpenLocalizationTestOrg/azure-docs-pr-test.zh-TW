---
title: "範例和常見案例 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 50df1e3db239a6aa34ac91bfbd582625c5b0041b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a><span data-ttu-id="9ca70-103">Azure Logic Apps 的範例和常見案例</span><span class="sxs-lookup"><span data-stu-id="9ca70-103">Examples and common scenarios for Azure Logic Apps</span></span>

<span data-ttu-id="9ca70-104">為了協助您深入了解 Azure Logic Apps 中的眾多模式和功能，以下提供了常見的範例與案例。</span><span class="sxs-lookup"><span data-stu-id="9ca70-104">To help you learn more about the many patterns and capabilities in Azure Logic Apps, here are common examples and scenarios.</span></span>

## <a name="key-scenarios-for-logic-apps"></a><span data-ttu-id="9ca70-105">邏輯應用程式的重要案例</span><span class="sxs-lookup"><span data-stu-id="9ca70-105">Key scenarios for logic apps</span></span>

<span data-ttu-id="9ca70-106">Azure Logic Apps 針對不同的服務提供了彈性的協調流程和整合功能。</span><span class="sxs-lookup"><span data-stu-id="9ca70-106">Azure Logic Apps provides resilient orchestration and integration for different services.</span></span> <span data-ttu-id="9ca70-107">Logic Apps 服務是「無伺服器」服務，因此您不必擔心調整或執行個體；您需要做的就只是定義工作流程 (觸發程序和動作)。</span><span class="sxs-lookup"><span data-stu-id="9ca70-107">The Logic Apps service is "serverless", so you don't have to worry about scale or instances - all you have to do is define the workflow (trigger and actions).</span></span> <span data-ttu-id="9ca70-108">基礎平台可處理調整、可用性和效能。</span><span class="sxs-lookup"><span data-stu-id="9ca70-108">The underlying platform handles scale, availability, and performance.</span></span> <span data-ttu-id="9ca70-109">只要是需要協調多個動作的案例 (尤其是跨多個系統時)，都是 Azure Logic Apps 的絕佳使用案例。</span><span class="sxs-lookup"><span data-stu-id="9ca70-109">Any scenario where you need to coordinate multiple actions, especially across multiple systems, is a great use case for Azure Logic Apps.</span></span> <span data-ttu-id="9ca70-110">以下有一些模式和範例。</span><span class="sxs-lookup"><span data-stu-id="9ca70-110">Here are some patterns and examples.</span></span>

## <a name="respond-to-triggers-and-extend-actions"></a><span data-ttu-id="9ca70-111">回應觸發程序並延伸動作</span><span class="sxs-lookup"><span data-stu-id="9ca70-111">Respond to triggers and extend actions</span></span>

<span data-ttu-id="9ca70-112">每個邏輯應用程式都會從觸發程序來開始。</span><span class="sxs-lookup"><span data-stu-id="9ca70-112">Every logic app begins with a trigger.</span></span> <span data-ttu-id="9ca70-113">例如，您的工作流程可以從排程事件、手動叫用或外部系統的事件 (例如「當檔案新增至 FTP 伺服器時」觸發程序) 來開始。</span><span class="sxs-lookup"><span data-stu-id="9ca70-113">For example, your workflow can start with a schedule event, a manual invocation, or an event from an external system, such as the "when a file is added to an FTP server" trigger.</span></span> <span data-ttu-id="9ca70-114">Azure Logic Apps 目前支援超過 100 個立即可用的連接器，範圍從內部部署 SAP 到 Microsoft 辨識服務。</span><span class="sxs-lookup"><span data-stu-id="9ca70-114">Azure Logic Apps currently supports over 100 ready-to-use connectors, ranging from on-premises SAP to Microsoft Cognitive Services.</span></span> <span data-ttu-id="9ca70-115">對於可能沒有已發佈連接器的系統和服務，您也可以延伸邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ca70-115">For systems and services that might not have published connectors, you can also extend logic apps.</span></span>

* [<span data-ttu-id="9ca70-116">建立自訂觸發程序或動作</span><span class="sxs-lookup"><span data-stu-id="9ca70-116">Create custom triggers or actions</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="9ca70-117">為工作流程執行設定長時間執行的動作</span><span class="sxs-lookup"><span data-stu-id="9ca70-117">Set up long-running actions for workflow runs</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="9ca70-118">使用 Webhook 回應外部事件和動作</span><span class="sxs-lookup"><span data-stu-id="9ca70-118">Respond to external events and actions with webhooks</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="9ca70-119">呼叫、觸發或巢狀處理具有 HTTP 要求同步回應的工作流程</span><span class="sxs-lookup"><span data-stu-id="9ca70-119">Call, trigger, or nest workflows with synchronous responses to HTTP requests</span></span>](../logic-apps/logic-apps-http-endpoint.md)
* [<span data-ttu-id="9ca70-120">教學課程︰回應 Twilio SMS Webhook 並傳送文字回應</span><span class="sxs-lookup"><span data-stu-id="9ca70-120">Tutorial: Respond to Twilio SMS webhooks and send a text response</span></span>](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [<span data-ttu-id="9ca70-121">教學課程︰使用 Logic Apps 和 Power BI 在幾分鐘內建置具有 AI 技術的社交儀表板</span><span class="sxs-lookup"><span data-stu-id="9ca70-121">Tutorial: Build an AI-powered social dashboard in minutes with Logic Apps and Power BI</span></span>](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a><span data-ttu-id="9ca70-122">錯誤處理、記錄和控制流程功能</span><span class="sxs-lookup"><span data-stu-id="9ca70-122">Error handling, logging, and control flow capabilities</span></span>

<span data-ttu-id="9ca70-123">邏輯應用程式包含豐富的功能，可用於處理進階控制流程，例如條件、開關、迴圈和範圍。</span><span class="sxs-lookup"><span data-stu-id="9ca70-123">Logic apps include rich capabilities for advanced control flow, like conditions, switches, loops, and scopes.</span></span> <span data-ttu-id="9ca70-124">若要確保解決方案的彈性，您也可以在工作流程中實作錯誤和例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="9ca70-124">To ensure resilient solutions, you can also implement error and exception handling in your workflows.</span></span> <span data-ttu-id="9ca70-125">針對工作流程執行狀態的通知和診斷記錄，Azure Logic Apps 也提供了監視和警示。</span><span class="sxs-lookup"><span data-stu-id="9ca70-125">For notification and diagnostic logs for workflow run status, Azure Logic Apps also provides monitoring and alerts.</span></span>

* [<span data-ttu-id="9ca70-126">使用 switch 陳述式來執行不同動作</span><span class="sxs-lookup"><span data-stu-id="9ca70-126">Perform different actions with switch statements</span></span>](../logic-apps/logic-apps-switch-case.md)
* [<span data-ttu-id="9ca70-127">在邏輯應用程式中使用迴圈和批次處理陣列和集合中的項目</span><span class="sxs-lookup"><span data-stu-id="9ca70-127">Process items in arrays and collections with loops and batches in logic apps</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="9ca70-128">在工作流程中撰寫錯誤和例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="9ca70-128">Author error and exception handling in a workflow</span></span>](../logic-apps/logic-apps-exception-handling.md)
* [<span data-ttu-id="9ca70-129">開啟現有 Logic Apps 的監視、記錄和警示</span><span class="sxs-lookup"><span data-stu-id="9ca70-129">Turn on monitoring, logging, and alerts for existing logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="9ca70-130">建立 Logic Apps 時開啟監視和診斷記錄</span><span class="sxs-lookup"><span data-stu-id="9ca70-130">Turn on monitoring and diagnostics logging when creating logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [<span data-ttu-id="9ca70-131">使用案例︰醫療保健公司如何使用邏輯應用程式的例外狀況處理來處理 HL7 FHIR 工作流程</span><span class="sxs-lookup"><span data-stu-id="9ca70-131">Use case: How a healthcare company uses logic app exception handling for HL7 FHIR workflows</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a><span data-ttu-id="9ca70-132">部署和管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="9ca70-132">Deploy and manage logic apps</span></span>

<span data-ttu-id="9ca70-133">您可以完全透過 Visual Studio、Visual Studio Team Services 或其他任何原始檔控制和自動化建置工具，來開發及部署邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ca70-133">You can fully develop and deploy logic apps with Visual Studio, Visual Studio Team Services, or any other source control and automated build tools.</span></span> <span data-ttu-id="9ca70-134">為了支援將工作流程與相依連線部署在資源範本中的功能，邏輯應用程式使用 Azure 資源部署範本。</span><span class="sxs-lookup"><span data-stu-id="9ca70-134">To support deployment for workflows and dependent connections in a resource template, logic apps use Azure resource deployment templates.</span></span> <span data-ttu-id="9ca70-135">Visual Studio 工具會自動產生這些範本，您可以將其簽入原始檔控制以便控制版本。</span><span class="sxs-lookup"><span data-stu-id="9ca70-135">Visual Studio tools automatically generate these templates, which you can check in to source control for versioning.</span></span>

* [<span data-ttu-id="9ca70-136">建立自動部署範本</span><span class="sxs-lookup"><span data-stu-id="9ca70-136">Create an automated deployment template</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="9ca70-137">在 Visual Studio 中建置和部署 Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9ca70-137">Build and deploy logic apps from Visual Studio</span></span>](../logic-apps/logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="9ca70-138">監視邏輯應用程式的健康狀態</span><span class="sxs-lookup"><span data-stu-id="9ca70-138">Monitor the health of your logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a><span data-ttu-id="9ca70-139">執行內的內容類型、轉換 (Conversion) 及轉換 (Transformation)</span><span class="sxs-lookup"><span data-stu-id="9ca70-139">Content types, conversions, and transformations within a run</span></span>

<span data-ttu-id="9ca70-140">您可以使用 Azure Logic Apps [工作流程定義語言](http://aka.ms/logicappsdocs)中的許多函數，來存取、轉換 (Convert) 及轉換 (Transform) 多種內容類型。</span><span class="sxs-lookup"><span data-stu-id="9ca70-140">You can access, convert, and transform multiple content types by using the many functions in the Azure Logic Apps [workflow definition language](http://aka.ms/logicappsdocs).</span></span> <span data-ttu-id="9ca70-141">例如，您可以使用 `@json()` 和 `@xml()` 工作流程運算式，在字串、JSON 和 XML 之間進行轉換 (Convert)。</span><span class="sxs-lookup"><span data-stu-id="9ca70-141">For example, you can convert between a string, JSON, and XML with the `@json()` and `@xml()` workflow expressions.</span></span> <span data-ttu-id="9ca70-142">Logic Apps 引擎會保留內容類型，以支援在服務之間以不失真的方式進行內容傳輸的功能。</span><span class="sxs-lookup"><span data-stu-id="9ca70-142">The Logic Apps engine preserves content types to support content transfer in a lossless manner between services.</span></span>

* <span data-ttu-id="9ca70-143">[處理非 JSON 內容類型](../logic-apps/logic-apps-content-type.md)，例如 `application/xml`、`application/octet-stream` 和 `multipart/formdata`</span><span class="sxs-lookup"><span data-stu-id="9ca70-143">[Handle non-JSON content types](../logic-apps/logic-apps-content-type.md), like `application/xml`, `application/octet-stream`, and `multipart/formdata`</span></span>
* [<span data-ttu-id="9ca70-144">工作流程運算式在邏輯應用程式中的運作方式</span><span class="sxs-lookup"><span data-stu-id="9ca70-144">How workflow expressions work in logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="9ca70-145">參考：Azure Logic Apps 工作流程定義語言</span><span class="sxs-lookup"><span data-stu-id="9ca70-145">Reference: Azure Logic Apps workflow definition language</span></span>](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a><span data-ttu-id="9ca70-146">其他整合和功能</span><span class="sxs-lookup"><span data-stu-id="9ca70-146">Other integrations and capabilities</span></span>

<span data-ttu-id="9ca70-147">邏輯應用程式也提供與許多服務 (例如 Azure Functions、Azure API 管理、Azure App Service) 和自訂 HTTP 端點 (例如 REST 和 SOAP) 的整合。</span><span class="sxs-lookup"><span data-stu-id="9ca70-147">Logic apps also offer integration with many services, like Azure Functions, Azure API Management, Azure App Services, and custom HTTP endpoints, for example, REST and SOAP.</span></span>

* [<span data-ttu-id="9ca70-148">使用 Azure 無伺服器建立即時社交儀表板</span><span class="sxs-lookup"><span data-stu-id="9ca70-148">Create a real-time social dashboard with Azure Serverless</span></span>](../logic-apps/logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="9ca70-149">從邏輯應用程式呼叫 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9ca70-149">Call Azure Functions from logic apps</span></span>](../logic-apps/logic-apps-azure-functions.md)
* [<span data-ttu-id="9ca70-150">案例：使用 Azure Functions 觸發邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="9ca70-150">Scenario: Trigger logic apps with Azure Functions</span></span>](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [<span data-ttu-id="9ca70-151">部落格︰從邏輯應用程式呼叫 SOAP 端點</span><span class="sxs-lookup"><span data-stu-id="9ca70-151">Blog: Call SOAP endpoints from logic apps</span></span>](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a><span data-ttu-id="9ca70-152">端對端案例</span><span class="sxs-lookup"><span data-stu-id="9ca70-152">End-to-end scenarios</span></span>

* [<span data-ttu-id="9ca70-153">白皮書：使用 Azure 服務 (例如 Logic Apps) 進行企業整合端對端案例管理</span><span class="sxs-lookup"><span data-stu-id="9ca70-153">Whitepaper: Enterprise integration end-to-end case management with Azure services, like Logic Apps</span></span>](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a><span data-ttu-id="9ca70-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ca70-154">Next steps</span></span>

- [<span data-ttu-id="9ca70-155">處理邏輯應用程式中的錯誤和例外狀況</span><span class="sxs-lookup"><span data-stu-id="9ca70-155">Handle errors and exceptions in logic apps</span></span>](../logic-apps/logic-apps-exception-handling.md)
- [<span data-ttu-id="9ca70-156">使用工作流程定義語言撰寫工作流程定義</span><span class="sxs-lookup"><span data-stu-id="9ca70-156">Author workflow definitions with the workflow definition language</span></span>](../logic-apps/logic-apps-author-definitions.md)
- [<span data-ttu-id="9ca70-157">提交有關我們該如何改善 Azure Logic Apps 的評論、問題、意見或建議</span><span class="sxs-lookup"><span data-stu-id="9ca70-157">Submit your comments, questions, feedback, or suggestions for how can we improve Azure Logic Apps</span></span>](https://feedback.azure.com/forums/287593-logic-apps)