---
title: "Logic Apps 連接器概觀 | Microsoft Docs"
description: "可在邏輯應用程式中使用的連接器概觀"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: 9cbb258ae9e32549669623e6824dd9b18fa1f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-connectors-in-a-logic-app"></a><span data-ttu-id="5789b-103">在邏輯應用程式中使用連接器</span><span class="sxs-lookup"><span data-stu-id="5789b-103">Using connectors in a logic app</span></span>
<span data-ttu-id="5789b-104">連接器可讓您跨服務、通訊協定與平台快速存取事件、資料和動作。</span><span class="sxs-lookup"><span data-stu-id="5789b-104">Connectors provide quick access to events, data, and actions across services, protocols, and platforms.</span></span>  <span data-ttu-id="5789b-105">Logic Apps 所支援的連接器完整清單可以 [在這裡找到](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="5789b-105">The full list of connectors that Logic Apps supports can [be found here](apis-list.md).</span></span>  <span data-ttu-id="5789b-106">連接器可做為邏輯應用程式的觸發程序或動作，而且可能需要設定「連線」  才能使用 (例如︰授權 Twitter 帳戶代表您存取或張貼)。</span><span class="sxs-lookup"><span data-stu-id="5789b-106">Connectors can be used as a trigger or an action in a logic app, and may require a configured *connection* to use (for example: authorizing a Twitter account to access or post on your behalf).</span></span>

## <a name="basics"></a><span data-ttu-id="5789b-107">基本</span><span class="sxs-lookup"><span data-stu-id="5789b-107">Basics</span></span>
<span data-ttu-id="5789b-108">連接器是邏輯應用程式中可供您存取以便整合 Dynamics、Azure、Salesforce [等等](apis-list.md)的其他服務的託管服務。</span><span class="sxs-lookup"><span data-stu-id="5789b-108">Connectors are hosted services you can access as part of a logic app to integrate with other services like Dynamics, Azure, Salesforce, [and more](apis-list.md).</span></span>  <span data-ttu-id="5789b-109">連接器是由 Microsoft 所部署和管理，因此您可以建置規模、輸送量和安全性都有人幫您處理的整合工作流程。</span><span class="sxs-lookup"><span data-stu-id="5789b-109">They are deployed and managed by Microsoft, so you can build your integration workflows with scale, throughput, and security taken care of.</span></span>  <span data-ttu-id="5789b-110">您可以藉由搜尋和選取 [顯示 Microsoft Managed API] 底下的連接器動作或觸發程序，在邏輯應用程式中新增連接器。</span><span class="sxs-lookup"><span data-stu-id="5789b-110">You can add a connector to a logic app by searching and selecting a connector action or trigger under **Show Microsoft managed APIs**.</span></span>

![可供選取觸發程序的 [動作] 功能表][1]

<span data-ttu-id="5789b-112">每個連接器動作或觸發程序都有需要設定的屬性集。</span><span class="sxs-lookup"><span data-stu-id="5789b-112">Each connector action or trigger will have its set of properties to configure.</span></span>  <span data-ttu-id="5789b-113">您可以按一下 [資訊] 按鈕來深入了解動作，或參考其文件以 [深入了解](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="5789b-113">You can click on the info buttons to learn more about action, or reference its documentation [to learn more](apis-list.md).</span></span>

<span data-ttu-id="5789b-114">如果您想要整合還未成為連接器的服務或 API，您也可以透過 [自訂連接器](../logic-apps/logic-apps-create-api-app.md) 擴充邏輯應用程式，或直接透過 HTTP 等通訊協定呼叫服務。</span><span class="sxs-lookup"><span data-stu-id="5789b-114">If you want to integrate with a service or API that isn't yet a connector, you can also extend logic apps through a [custom connector](../logic-apps/logic-apps-create-api-app.md) or just call directly to the service over a protocol like HTTP.</span></span>

## <a name="triggers"></a><span data-ttu-id="5789b-115">觸發程序</span><span class="sxs-lookup"><span data-stu-id="5789b-115">Triggers</span></span>
<span data-ttu-id="5789b-116">某些連接器具有觸發程序，這表示該連接器中的事件會引發邏輯應用程式，並傳入任何資料做為觸發程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="5789b-116">Some connectors have a trigger, which means an event from that connector will fire a logic app and pass in any data as part of the trigger.</span></span>  <span data-ttu-id="5789b-117">觸發程序永遠是邏輯應用程式的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5789b-117">A trigger is always the first step in a logic app.</span></span>  <span data-ttu-id="5789b-118">受歡迎的觸發程序所包含的作業如下︰</span><span class="sxs-lookup"><span data-stu-id="5789b-118">Popular triggers include operations like:</span></span>

* <span data-ttu-id="5789b-119">循環 - 每小時執行一次</span><span class="sxs-lookup"><span data-stu-id="5789b-119">Recurrence - run every hour</span></span>
* <span data-ttu-id="5789b-120">收到 HTTP 要求時</span><span class="sxs-lookup"><span data-stu-id="5789b-120">When an HTTP request is received</span></span>
* <span data-ttu-id="5789b-121">佇列中新增項目時</span><span class="sxs-lookup"><span data-stu-id="5789b-121">When an item is added to a queue</span></span>
* <span data-ttu-id="5789b-122">收到電子郵件時</span><span class="sxs-lookup"><span data-stu-id="5789b-122">When an email is received</span></span>

<span data-ttu-id="5789b-123">在事件發生當下，有些觸發程序會在邏輯應用程式收到通知時立刻引發，有些則需要設定循環間隔，以指出邏輯應用程式檢查服務是否發生事件的頻率 (最多為每 15 秒)。</span><span class="sxs-lookup"><span data-stu-id="5789b-123">Some triggers will fire the instant an event happens through a notification to the logic app, and others will need a recurrence interval configured on how often the logic app will check the service for an event (up to every 15 seconds).</span></span>  

<span data-ttu-id="5789b-124">一旦收到事件，就會引發執行邏輯應用程式，並開始工作流程中的動作。</span><span class="sxs-lookup"><span data-stu-id="5789b-124">Once an event is received, the logic app run will fire and the actions in the workflow will start.</span></span>  <span data-ttu-id="5789b-125">您也可以在整個工作流程存取觸發程序的任何資料 (例如，「有新推文時」觸發程序會讓推文進入執行狀態)。</span><span class="sxs-lookup"><span data-stu-id="5789b-125">You will also be able to access any data from the trigger throughout the workflow (for example the 'On a new tweet' trigger will pass the tweet into the run).</span></span>

## <a name="actions"></a><span data-ttu-id="5789b-126">動作</span><span class="sxs-lookup"><span data-stu-id="5789b-126">Actions</span></span>
<span data-ttu-id="5789b-127">大部分連接器有一或多個可做為工作流程一部分來執行的動作。</span><span class="sxs-lookup"><span data-stu-id="5789b-127">Most connectors have one or many actions that can be executed as part of the workflow.</span></span>  <span data-ttu-id="5789b-128">動作是觸發程序已引發該次執行之後所發生的任何步驟。</span><span class="sxs-lookup"><span data-stu-id="5789b-128">Actions are any steps that happen after the run has fired from a trigger.</span></span>  <span data-ttu-id="5789b-129">若要新增動作，請按一下 [新增步驟]  按鈕，並搜尋您想要使用的連接器。</span><span class="sxs-lookup"><span data-stu-id="5789b-129">To add an action click the **New Step** button and search for the connector you want to use.</span></span>  <span data-ttu-id="5789b-130">一經選取 (以及在設定任何可能需要的 [連線](#connections) 之後)，您就會看到可以設定的動作卡。</span><span class="sxs-lookup"><span data-stu-id="5789b-130">Once selected (and after configuring any [connections](#connections) that may be required) you will see the action card you can configure.</span></span>  <span data-ttu-id="5789b-131">您可以按一下輸出的任何權杖以選取先前步驟的資料，或視需要輸入其他任何組態。</span><span class="sxs-lookup"><span data-stu-id="5789b-131">You can select data from previous steps by clicking on any of the tokens for outputs, or enter in any other configuration as needed.</span></span>

![設定連接器動作][2]

## <a name="connections"></a><span data-ttu-id="5789b-133">連線</span><span class="sxs-lookup"><span data-stu-id="5789b-133">Connections</span></span>
<span data-ttu-id="5789b-134">大部分連接器都必須先設定「連線」  然後才可供使用。</span><span class="sxs-lookup"><span data-stu-id="5789b-134">Most connectors require you to configure a *connection* before you can use the connector.</span></span>  <span data-ttu-id="5789b-135">「連線」  是用來存取連接器所需的任何登入或連接組態。</span><span class="sxs-lookup"><span data-stu-id="5789b-135">A *connection* is any login or connection configuration needed to access the connector.</span></span>  <span data-ttu-id="5789b-136">對於使用 OAuth 的連接器，建立連線表示登入服務 (例如 Office 365、Salesforce 或 GitHub)，而您的存取權杖可加密並安全地儲存在 Azure 的密碼存放區。</span><span class="sxs-lookup"><span data-stu-id="5789b-136">For connectors that use OAuth, create a connection means signing into the service (like Office 365, Salesforce, or GitHub) where your access token can be encrypted and securely stored in an Azure secret store.</span></span>  <span data-ttu-id="5789b-137">其他連接器 (例如 FTP 和 SQL) 則需要包含伺服器位址、使用者名稱和密碼等組態的連線。</span><span class="sxs-lookup"><span data-stu-id="5789b-137">Other connectors (like FTP and SQL) require a connection that contains configuration like server address, username, and password.</span></span>  <span data-ttu-id="5789b-138">這些連線的組態詳細資料也會加密並安全地儲存。</span><span class="sxs-lookup"><span data-stu-id="5789b-138">These connection configuration details are also encrypted and securely stored.</span></span>  <span data-ttu-id="5789b-139">只要在服務所允許的時間內，連線均可存取服務。</span><span class="sxs-lookup"><span data-stu-id="5789b-139">Connections will be able to access the service for as long as the service allows.</span></span>  <span data-ttu-id="5789b-140">針對 Azure Active Directory OAuth 連線 (例如 Office 365 和 Dynamics)，我們可以無限期地不斷重新整理存取權杖。</span><span class="sxs-lookup"><span data-stu-id="5789b-140">For Azure Active Directory OAuth connections (like Office 365 and Dynamics) we can continue to refresh the access token indefinitely.</span></span>  <span data-ttu-id="5789b-141">其他服務則可能會限制權杖的使用時限，在此時限內，完全不需要重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="5789b-141">Other services may put limits on how long we can use a token without it being refreshed.</span></span>  <span data-ttu-id="5789b-142">一般來說，某些動作 (例如變更密碼) 會導致所有存取權杖失效。</span><span class="sxs-lookup"><span data-stu-id="5789b-142">In general certain actions like changing a password will invalidate all access tokens.</span></span>  

<span data-ttu-id="5789b-143">按一下 [瀏覽]，然後選取 [API 連線]，即可在 Azure 中檢視和管理連線。</span><span class="sxs-lookup"><span data-stu-id="5789b-143">Connections can be viewed and managed in Azure by clicking **Browse** and selecting **API Connections**.</span></span>  <span data-ttu-id="5789b-144">在 API 連線資源中，您可以檢視、編輯、更新或重新授權任何已建立的連線。</span><span class="sxs-lookup"><span data-stu-id="5789b-144">From the API Connections resource you can view, edit, update, or re-authorize any connections you have created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5789b-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5789b-145">Next Steps</span></span>
* [<span data-ttu-id="5789b-146">建立第一個邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="5789b-146">Create your first logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="5789b-147">了解邏輯應用程式的常見用法和範例</span><span class="sxs-lookup"><span data-stu-id="5789b-147">Learn common uses and examples of logic apps</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="5789b-148">開始使用企業整合觸發程序和動作</span><span class="sxs-lookup"><span data-stu-id="5789b-148">Get started with enterprise integration triggers and actions</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
