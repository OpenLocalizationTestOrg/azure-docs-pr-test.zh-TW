---
title: "在 Azure Logic Apps 中使用 Slack 連接器 | Microsoft Docs"
description: "連接至 Logic Apps 中的 Slack"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: fc5fc128efe01bd0727e3ff30d8938918e89ac3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="64f01-103">開始使用 Slack 連接器</span><span class="sxs-lookup"><span data-stu-id="64f01-103">Get started with the Slack connector</span></span>
<span data-ttu-id="64f01-104">Slack 是團隊通訊工具，能把您團隊的通訊都集中在一個地方，讓您不但在何處都可使用，還能搜尋各項記錄。</span><span class="sxs-lookup"><span data-stu-id="64f01-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="64f01-105">立即開始建立邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="64f01-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="64f01-106">建立至 Slack 的連線</span><span class="sxs-lookup"><span data-stu-id="64f01-106">Create a connection to Slack</span></span>
<span data-ttu-id="64f01-107">如要使用 Slack 連接器，您必須先建立 **連線** ，然後提供下列屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="64f01-107">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="64f01-108">屬性</span><span class="sxs-lookup"><span data-stu-id="64f01-108">Property</span></span> | <span data-ttu-id="64f01-109">必要</span><span class="sxs-lookup"><span data-stu-id="64f01-109">Required</span></span> | <span data-ttu-id="64f01-110">說明</span><span class="sxs-lookup"><span data-stu-id="64f01-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64f01-111">權杖</span><span class="sxs-lookup"><span data-stu-id="64f01-111">Token</span></span> |<span data-ttu-id="64f01-112">是</span><span class="sxs-lookup"><span data-stu-id="64f01-112">Yes</span></span> |<span data-ttu-id="64f01-113">提供 Slack 的認證</span><span class="sxs-lookup"><span data-stu-id="64f01-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="64f01-114">請遵循下列步驟登入 Slack，並在邏輯應用程式中完成 Slack **連線** 設定：</span><span class="sxs-lookup"><span data-stu-id="64f01-114">Follow these steps to sign into Slack, and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="64f01-115">選取 [週期] </span><span class="sxs-lookup"><span data-stu-id="64f01-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="64f01-116">選取 [頻率] 並輸入 [間隔]</span><span class="sxs-lookup"><span data-stu-id="64f01-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="64f01-117">選取 [新增動作]</span><span class="sxs-lookup"><span data-stu-id="64f01-117">Select **Add an action**</span></span>  
   <span data-ttu-id="64f01-118">![設定 Slack][1]</span><span class="sxs-lookup"><span data-stu-id="64f01-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="64f01-119">在搜尋方塊中輸入 Slack，並等候搜尋傳回所有名稱中有 Slack 的項目</span><span class="sxs-lookup"><span data-stu-id="64f01-119">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="64f01-120">選取 [Slack - 張貼訊息] </span><span class="sxs-lookup"><span data-stu-id="64f01-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="64f01-121">選取 [登入 Slack]：</span><span class="sxs-lookup"><span data-stu-id="64f01-121">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="64f01-122">![設定 Slack][2]</span><span class="sxs-lookup"><span data-stu-id="64f01-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="64f01-123">提供您的 Slack 認證來登入並授權應用程式</span><span class="sxs-lookup"><span data-stu-id="64f01-123">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![設定 Slack][3]  
8. <span data-ttu-id="64f01-125">您將會重新導向至組織的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="64f01-125">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="64f01-126">**授權** Slack 與邏輯應用程式互動：</span><span class="sxs-lookup"><span data-stu-id="64f01-126">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="64f01-127">![設定 Slack][5]</span><span class="sxs-lookup"><span data-stu-id="64f01-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="64f01-128">驗證完成後，您會被重新導向至邏輯應用程式，設定 [Slack - 取得所有訊息]  區段後，即可完成動作。</span><span class="sxs-lookup"><span data-stu-id="64f01-128">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="64f01-129">加入其他所需的觸發和動作。</span><span class="sxs-lookup"><span data-stu-id="64f01-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="64f01-130">![設定 Slack][6]</span><span class="sxs-lookup"><span data-stu-id="64f01-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="64f01-131">選取上方功能表列的 [儲存]  來儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="64f01-131">Save your work by selecting **Save** on the menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="64f01-132">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="64f01-132">Connector-specific details</span></span>

<span data-ttu-id="64f01-133">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/slack/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="64f01-133">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="64f01-134">其他連接器</span><span class="sxs-lookup"><span data-stu-id="64f01-134">More connectors</span></span>
<span data-ttu-id="64f01-135">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="64f01-135">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
