---
title: "Azure Logic Apps 中的 GitHub 連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 GitHub 是 Web 架構的 Git 儲存機制裝載服務。 它提供所有 Git 分散式修訂控制項和來源程式碼管理 (SCM) 功能，也加入自己的功能。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="3a44b-105">開始使用 GitHub 連接器</span><span class="sxs-lookup"><span data-stu-id="3a44b-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="3a44b-106">GitHub 是 Web 架構的 Git 儲存機制裝載服務。</span><span class="sxs-lookup"><span data-stu-id="3a44b-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="3a44b-107">它提供所有 Git 分散式修訂控制項和來源程式碼管理 (SCM) 功能，也加入自己的功能。</span><span class="sxs-lookup"><span data-stu-id="3a44b-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="3a44b-108">您可以從建立邏輯應用程式立即開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="3a44b-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="3a44b-109">建立 GitHub 的連線</span><span class="sxs-lookup"><span data-stu-id="3a44b-109">Create a connection to GitHub</span></span>
<span data-ttu-id="3a44b-110">若要使用 GitHub 建立邏輯應用程式，您必須先建立**連接**，然後提供下列屬性的詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="3a44b-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="3a44b-111">屬性</span><span class="sxs-lookup"><span data-stu-id="3a44b-111">Property</span></span> | <span data-ttu-id="3a44b-112">必要</span><span class="sxs-lookup"><span data-stu-id="3a44b-112">Required</span></span> | <span data-ttu-id="3a44b-113">說明</span><span class="sxs-lookup"><span data-stu-id="3a44b-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a44b-114">權杖</span><span class="sxs-lookup"><span data-stu-id="3a44b-114">Token</span></span> |<span data-ttu-id="3a44b-115">是</span><span class="sxs-lookup"><span data-stu-id="3a44b-115">Yes</span></span> |<span data-ttu-id="3a44b-116">提供 GitHub 認證</span><span class="sxs-lookup"><span data-stu-id="3a44b-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="3a44b-117">建立連線後，您就可以用它執行動作，並接聽本文所述的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="3a44b-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="3a44b-118">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="3a44b-118">Connector-specific details</span></span>

<span data-ttu-id="3a44b-119">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/github/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="3a44b-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="3a44b-120">其他連接器</span><span class="sxs-lookup"><span data-stu-id="3a44b-120">More connectors</span></span>
<span data-ttu-id="3a44b-121">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="3a44b-121">Go back to the [APIs list](apis-list.md).</span></span>