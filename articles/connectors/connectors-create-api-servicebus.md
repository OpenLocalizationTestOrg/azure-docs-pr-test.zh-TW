---
title: "在您的 logic apps aaaLearn toouse hello Azure 服務匯流排連接器 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooAzure Service Bus toosend 和接收訊息。 您可以執行動作，例如傳送 tooqueue、 傳送 tootopic、 接收來自佇列，及接收來自訂用帳戶。"
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
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="f719c-105">開始使用 hello Azure 服務匯流排連接器</span><span class="sxs-lookup"><span data-stu-id="f719c-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="f719c-106">連接 tooAzure Service Bus toosend 和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="f719c-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="f719c-107">您可以執行動作，例如傳送 tooqueue、 傳送 tootopic、 接收來自佇列，及接收來自訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f719c-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="f719c-108">toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f719c-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="f719c-109">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="f719c-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="f719c-110">連接 tooService 匯流排</span><span class="sxs-lookup"><span data-stu-id="f719c-110">Connect tooService Bus</span></span>
<span data-ttu-id="f719c-111">邏輯應用程式可以存取任何服務之前，您必須先 toocreate 連接 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="f719c-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="f719c-112">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="f719c-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="f719c-113">使用服務匯流排觸發程序</span><span class="sxs-lookup"><span data-stu-id="f719c-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="f719c-114">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="f719c-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="f719c-115">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="f719c-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="f719c-116">使用服務匯流排動作</span><span class="sxs-lookup"><span data-stu-id="f719c-116">Use a Service Bus action</span></span>
<span data-ttu-id="f719c-117">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="f719c-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="f719c-118">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="f719c-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="f719c-119">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="f719c-119">Connector-specific details</span></span>

<span data-ttu-id="f719c-120">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/servicebus/)。</span><span class="sxs-lookup"><span data-stu-id="f719c-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f719c-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f719c-121">Next steps</span></span>
<span data-ttu-id="f719c-122">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f719c-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

