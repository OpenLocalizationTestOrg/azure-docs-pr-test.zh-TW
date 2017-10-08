---
title: "aaaLearn toouse hello Salesforce 連接器，在您的 logic apps |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 hello Salesforce 連接器提供的 API toowork Salesforce 物件。"
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
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="081fa-104">開始使用 hello Salesforce 連接器</span><span class="sxs-lookup"><span data-stu-id="081fa-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="081fa-105">hello Salesforce 連接器提供的 API toowork Salesforce 物件。</span><span class="sxs-lookup"><span data-stu-id="081fa-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="081fa-106">toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="081fa-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="081fa-107">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="081fa-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="081fa-108">連接 tooSalesforce 連接器</span><span class="sxs-lookup"><span data-stu-id="081fa-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="081fa-109">邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="081fa-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="081fa-110">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="081fa-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="081fa-111">建立連接 tooSalesforce 連接器</span><span class="sxs-lookup"><span data-stu-id="081fa-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="081fa-112">使用 Salesforce 連接器觸發程序</span><span class="sxs-lookup"><span data-stu-id="081fa-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="081fa-113">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="081fa-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="081fa-114">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="081fa-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="081fa-115">新增條件</span><span class="sxs-lookup"><span data-stu-id="081fa-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="081fa-116">使用 Salesforce 連接器動作</span><span class="sxs-lookup"><span data-stu-id="081fa-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="081fa-117">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="081fa-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="081fa-118">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="081fa-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="081fa-119">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="081fa-119">Connector-specific details</span></span>

<span data-ttu-id="081fa-120">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/salesforce/)。</span><span class="sxs-lookup"><span data-stu-id="081fa-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="081fa-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="081fa-121">Next steps</span></span>
[<span data-ttu-id="081fa-122">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="081fa-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

