---
title: "Azure Logic Apps 中的 Wunderlist 連接器 | Microsoft Docs"
description: "建立 Wunderlist 連線，並使用此連線在 Logic Apps 中建置工作流程。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 899110992cc52ca5edf1706320fd5570473de784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-wunderlist-connector"></a><span data-ttu-id="6175b-103">開始使用 Wunderlist 連接器</span><span class="sxs-lookup"><span data-stu-id="6175b-103">Get started with the Wunderlist connector</span></span>
<span data-ttu-id="6175b-104">Wunderlist 提供待辦事項清單和工作管理員，協助使用者完成其工作。</span><span class="sxs-lookup"><span data-stu-id="6175b-104">Wunderlist provide a todo list and task manager to help people get their stuff done.</span></span>  <span data-ttu-id="6175b-105">無論是與親愛的人共用購物清單、處理專案，還是計劃假期，Wunderlist 都能讓您輕鬆擷取、共用及完成待辦事項。</span><span class="sxs-lookup"><span data-stu-id="6175b-105">Whether you’re sharing a grocery list with a loved one, working on a project, or planning a vacation, Wunderlist makes it easy to capture, share, and complete your to¬dos.</span></span> <span data-ttu-id="6175b-106">Wunderlist 立即同步處理您的電話、平板電腦及電腦，讓您可在任何地方存取工作。</span><span class="sxs-lookup"><span data-stu-id="6175b-106">Wunderlist instantly syncs between your phone, tablet and computer, so you can access all your tasks from anywhere.</span></span>

<span data-ttu-id="6175b-107">立即開始建立邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="6175b-107">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-wunderlist"></a><span data-ttu-id="6175b-108">建立 Wunderlist 的連線</span><span class="sxs-lookup"><span data-stu-id="6175b-108">Create a connection to Wunderlist</span></span>
<span data-ttu-id="6175b-109">若要使用 Wunderlist 建立邏輯應用程式，您必須先建立**連接**，然後提供下列屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="6175b-109">To create Logic apps with Wunderlist, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="6175b-110">屬性</span><span class="sxs-lookup"><span data-stu-id="6175b-110">Property</span></span> | <span data-ttu-id="6175b-111">必要</span><span class="sxs-lookup"><span data-stu-id="6175b-111">Required</span></span> | <span data-ttu-id="6175b-112">說明</span><span class="sxs-lookup"><span data-stu-id="6175b-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6175b-113">權杖</span><span class="sxs-lookup"><span data-stu-id="6175b-113">Token</span></span> |<span data-ttu-id="6175b-114">是</span><span class="sxs-lookup"><span data-stu-id="6175b-114">Yes</span></span> |<span data-ttu-id="6175b-115">提供 Wunderlist 認證</span><span class="sxs-lookup"><span data-stu-id="6175b-115">Provide Wunderlist Credentials</span></span> |

<span data-ttu-id="6175b-116">建立連線後，您就可以用它執行動作，並接聽觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6175b-116">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Wunderlist](../../includes/connectors-create-api-wunderlist.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="6175b-117">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="6175b-117">Connector-specific details</span></span>

<span data-ttu-id="6175b-118">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/wunderlist/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="6175b-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/wunderlist/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="6175b-119">其他連接器</span><span class="sxs-lookup"><span data-stu-id="6175b-119">More connectors</span></span>
<span data-ttu-id="6175b-120">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="6175b-120">Go back to the [APIs list](apis-list.md).</span></span>