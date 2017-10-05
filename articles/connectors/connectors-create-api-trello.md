---
title: "Azure Logic Apps 中的 Trello 連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 Trello 讓您無論在辦公室及在家都能管理所有專案。  您可以用簡單、免費、具彈性且以視覺的方式來管理專案並組織所有項目。  連線到 Trello 以管理面板、清單和卡片"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: fe7a4377-5c24-4f72-ab1a-6d9d23e8d895
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 526a14710f24ee4a4b61a11873aa6caa0b47dc10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-trello-connector"></a><span data-ttu-id="6c8b3-106">開始使用 Trello 連接器</span><span class="sxs-lookup"><span data-stu-id="6c8b3-106">Get started with the Trello connector</span></span>
<span data-ttu-id="6c8b3-107">Trello 讓您無論在辦公室及在家都能管理所有專案。</span><span class="sxs-lookup"><span data-stu-id="6c8b3-107">Trello gives you perspective over all your projects, at work and at home.</span></span>  <span data-ttu-id="6c8b3-108">您可以用簡單、免費、具彈性且以視覺的方式來管理專案並組織所有項目。</span><span class="sxs-lookup"><span data-stu-id="6c8b3-108">It is an easy, free, flexible, and visual way to manage your projects and organize anything.</span></span>  <span data-ttu-id="6c8b3-109">連線到 Trello 以管理面板、清單和卡片。</span><span class="sxs-lookup"><span data-stu-id="6c8b3-109">Connect to Trello to manage your boards, lists and cards.</span></span>

<span data-ttu-id="6c8b3-110">從建立邏輯應用程式開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="6c8b3-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-trello"></a><span data-ttu-id="6c8b3-111">建立至 Trello 的連線</span><span class="sxs-lookup"><span data-stu-id="6c8b3-111">Create a connection to Trello</span></span>
<span data-ttu-id="6c8b3-112">若要使用 Trello 建立 Logic Apps，請先建立**連接**，然後輸入下列屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="6c8b3-112">To create Logic apps with Trello, first create a **connection**, and enter the details for the following properties:</span></span>

| <span data-ttu-id="6c8b3-113">屬性</span><span class="sxs-lookup"><span data-stu-id="6c8b3-113">Property</span></span> | <span data-ttu-id="6c8b3-114">必要</span><span class="sxs-lookup"><span data-stu-id="6c8b3-114">Required</span></span> | <span data-ttu-id="6c8b3-115">說明</span><span class="sxs-lookup"><span data-stu-id="6c8b3-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c8b3-116">權杖</span><span class="sxs-lookup"><span data-stu-id="6c8b3-116">Token</span></span> |<span data-ttu-id="6c8b3-117">是</span><span class="sxs-lookup"><span data-stu-id="6c8b3-117">Yes</span></span> |<span data-ttu-id="6c8b3-118">提供 Trello 認證</span><span class="sxs-lookup"><span data-stu-id="6c8b3-118">Provide Trello Credentials</span></span> |

<span data-ttu-id="6c8b3-119">建立連線後，您就可以用它執行動作，並接聽觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6c8b3-119">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Trello](../../includes/connectors-create-api-trello.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="6c8b3-120">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="6c8b3-120">Connector-specific details</span></span>

<span data-ttu-id="6c8b3-121">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/trello/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="6c8b3-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/trello/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="6c8b3-122">其他連接器</span><span class="sxs-lookup"><span data-stu-id="6c8b3-122">More connectors</span></span>
<span data-ttu-id="6c8b3-123">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="6c8b3-123">Go back to the [APIs list](apis-list.md).</span></span>