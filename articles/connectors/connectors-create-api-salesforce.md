---
title: "了解在邏輯應用程式中使用 Salesforce 連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 Salesforce 連接器提供搭配 Salesforce 物件使用的 API。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="e638b-104">開始使用 Salesforce 連接器</span><span class="sxs-lookup"><span data-stu-id="e638b-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="e638b-105">Salesforce 連接器提供搭配 Salesforce 物件使用的 API。</span><span class="sxs-lookup"><span data-stu-id="e638b-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="e638b-106">若要使用[任何連接器](apis-list.md)，您必須先建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e638b-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="e638b-107">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="e638b-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="e638b-108">連接至 Salesforce 連接器</span><span class="sxs-lookup"><span data-stu-id="e638b-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="e638b-109">您必須先建立與服務的連線，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="e638b-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="e638b-110">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="e638b-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="e638b-111">建立至 Salesforce 連接器的連線</span><span class="sxs-lookup"><span data-stu-id="e638b-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="e638b-112">使用 Salesforce 連接器觸發程序</span><span class="sxs-lookup"><span data-stu-id="e638b-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="e638b-113">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="e638b-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="e638b-114">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="e638b-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="e638b-115">新增條件</span><span class="sxs-lookup"><span data-stu-id="e638b-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="e638b-116">使用 Salesforce 連接器動作</span><span class="sxs-lookup"><span data-stu-id="e638b-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="e638b-117">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="e638b-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="e638b-118">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="e638b-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="e638b-119">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="e638b-119">Connector-specific details</span></span>

<span data-ttu-id="e638b-120">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/salesforce/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="e638b-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e638b-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e638b-121">Next steps</span></span>
[<span data-ttu-id="e638b-122">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="e638b-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

