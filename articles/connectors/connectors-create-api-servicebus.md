---
title: "了解在您的邏輯應用程式中使用 Azure 服務匯流排連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 連線到 Azure 服務匯流排來傳送及接收訊息。 您可以執行動作，例如傳送至佇列、傳送至主題、從佇列接收和從訂用帳戶接收。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1e2ce06f5993280dbdb67121849591e67f7979e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-service-bus-connector"></a><span data-ttu-id="609d7-105">開始使用 Azure 服務匯流排連接器</span><span class="sxs-lookup"><span data-stu-id="609d7-105">Get started with the Azure Service Bus connector</span></span>
<span data-ttu-id="609d7-106">連線到 Azure 服務匯流排來傳送及接收訊息。</span><span class="sxs-lookup"><span data-stu-id="609d7-106">Connect to Azure Service Bus to send and receive messages.</span></span> <span data-ttu-id="609d7-107">您可以執行動作，例如傳送至佇列、傳送至主題、從佇列接收和從訂用帳戶接收。</span><span class="sxs-lookup"><span data-stu-id="609d7-107">You can perform actions such as send to queue, send to topic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="609d7-108">若要使用[任何連接器](apis-list.md)，您必須先建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="609d7-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="609d7-109">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="609d7-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-service-bus"></a><span data-ttu-id="609d7-110">連接到服務匯流排</span><span class="sxs-lookup"><span data-stu-id="609d7-110">Connect to Service Bus</span></span>
<span data-ttu-id="609d7-111">您必須先建立與服務的連線，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="609d7-111">Before your logic app can access any service, you first need to create a connection to the service.</span></span> <span data-ttu-id="609d7-112">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="609d7-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps to create a connection to Azure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="609d7-113">使用服務匯流排觸發程序</span><span class="sxs-lookup"><span data-stu-id="609d7-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="609d7-114">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="609d7-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="609d7-115">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="609d7-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="609d7-116">使用服務匯流排動作</span><span class="sxs-lookup"><span data-stu-id="609d7-116">Use a Service Bus action</span></span>
<span data-ttu-id="609d7-117">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="609d7-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="609d7-118">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="609d7-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps to create a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="609d7-119">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="609d7-119">Connector-specific details</span></span>

<span data-ttu-id="609d7-120">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/servicebus/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="609d7-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="609d7-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="609d7-121">Next steps</span></span>
<span data-ttu-id="609d7-122">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="609d7-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

