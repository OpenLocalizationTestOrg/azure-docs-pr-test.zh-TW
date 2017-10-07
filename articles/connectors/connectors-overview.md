---
title: "邏輯應用程式連接器的 aaaOverview |Microsoft 文件"
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
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a><span data-ttu-id="bd368-103">在邏輯應用程式中使用連接器</span><span class="sxs-lookup"><span data-stu-id="bd368-103">Using connectors in a logic app</span></span>
<span data-ttu-id="bd368-104">連接器會提供跨服務、 通訊協定和平台快速存取 tooevents、 資料和動作。</span><span class="sxs-lookup"><span data-stu-id="bd368-104">Connectors provide quick access tooevents, data, and actions across services, protocols, and platforms.</span></span>  <span data-ttu-id="bd368-105">hello 的 Logic Apps 支援的連接器的完整清單可以[在這裡找到](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="bd368-105">hello full list of connectors that Logic Apps supports can [be found here](apis-list.md).</span></span>  <span data-ttu-id="bd368-106">連接器可用來當作觸發程序或邏輯應用程式中的動作，而且可能需要設定*連接*toouse (例如： 授權 Twitter 帳戶 tooaccess 或張貼您的身分)。</span><span class="sxs-lookup"><span data-stu-id="bd368-106">Connectors can be used as a trigger or an action in a logic app, and may require a configured *connection* toouse (for example: authorizing a Twitter account tooaccess or post on your behalf).</span></span>

## <a name="basics"></a><span data-ttu-id="bd368-107">基本概念</span><span class="sxs-lookup"><span data-stu-id="bd368-107">Basics</span></span>
<span data-ttu-id="bd368-108">連接器是託管的服務，您可以存取 Dynamics、 Azure、 Salesforce 等其他服務使用邏輯應用程式 toointegrate 一部分[多](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="bd368-108">Connectors are hosted services you can access as part of a logic app toointegrate with other services like Dynamics, Azure, Salesforce, [and more](apis-list.md).</span></span>  <span data-ttu-id="bd368-109">連接器是由 Microsoft 所部署和管理，因此您可以建置規模、輸送量和安全性都有人幫您處理的整合工作流程。</span><span class="sxs-lookup"><span data-stu-id="bd368-109">They are deployed and managed by Microsoft, so you can build your integration workflows with scale, throughput, and security taken care of.</span></span>  <span data-ttu-id="bd368-110">您可以藉由搜尋並選取 連接器動作新增連接器 tooa 邏輯應用程式或觸發程序底下**顯示 Microsoft managed Api**。</span><span class="sxs-lookup"><span data-stu-id="bd368-110">You can add a connector tooa logic app by searching and selecting a connector action or trigger under **Show Microsoft managed APIs**.</span></span>

![可供選取觸發程序的 [動作] 功能表][1]

<span data-ttu-id="bd368-112">每個連接器動作或觸發程序會將屬性 tooconfigure 的設定。</span><span class="sxs-lookup"><span data-stu-id="bd368-112">Each connector action or trigger will have its set of properties tooconfigure.</span></span>  <span data-ttu-id="bd368-113">您可以按一下 hello 資訊按鈕 toolearn 深入了解動作，或參考其文件[toolearn 詳細](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="bd368-113">You can click on hello info buttons toolearn more about action, or reference its documentation [toolearn more](apis-list.md).</span></span>

<span data-ttu-id="bd368-114">如果您想 toointegrate 與服務或應用程式開發介面不是尚未連接器，您也可以擴充邏輯應用程式透過[自訂連接器](../logic-apps/logic-apps-create-api-app.md)或只需要呼叫直接 toohello 服務透過 HTTP 之類的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="bd368-114">If you want toointegrate with a service or API that isn't yet a connector, you can also extend logic apps through a [custom connector](../logic-apps/logic-apps-create-api-app.md) or just call directly toohello service over a protocol like HTTP.</span></span>

## <a name="triggers"></a><span data-ttu-id="bd368-115">觸發程序</span><span class="sxs-lookup"><span data-stu-id="bd368-115">Triggers</span></span>
<span data-ttu-id="bd368-116">某些連接器有觸發程序，這表示從該連接器的事件將引發邏輯應用程式，並傳入 hello 觸發程序的一部分的任何資料。</span><span class="sxs-lookup"><span data-stu-id="bd368-116">Some connectors have a trigger, which means an event from that connector will fire a logic app and pass in any data as part of hello trigger.</span></span>  <span data-ttu-id="bd368-117">觸發程序永遠是 hello 邏輯應用程式中的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="bd368-117">A trigger is always hello first step in a logic app.</span></span>  <span data-ttu-id="bd368-118">受歡迎的觸發程序所包含的作業如下︰</span><span class="sxs-lookup"><span data-stu-id="bd368-118">Popular triggers include operations like:</span></span>

* <span data-ttu-id="bd368-119">循環 - 每小時執行一次</span><span class="sxs-lookup"><span data-stu-id="bd368-119">Recurrence - run every hour</span></span>
* <span data-ttu-id="bd368-120">收到 HTTP 要求時</span><span class="sxs-lookup"><span data-stu-id="bd368-120">When an HTTP request is received</span></span>
* <span data-ttu-id="bd368-121">項目加入 tooa 佇列中時</span><span class="sxs-lookup"><span data-stu-id="bd368-121">When an item is added tooa queue</span></span>
* <span data-ttu-id="bd368-122">收到電子郵件時</span><span class="sxs-lookup"><span data-stu-id="bd368-122">When an email is received</span></span>

<span data-ttu-id="bd368-123">某些觸發程序會引發 hello 即時事件發生時透過通知 toohello 邏輯應用程式和其他人將會需要 hello 邏輯應用程式會檢查的頻率 （向上 tooevery 15 秒) 事件的 hello 服務上設定循環間隔。</span><span class="sxs-lookup"><span data-stu-id="bd368-123">Some triggers will fire hello instant an event happens through a notification toohello logic app, and others will need a recurrence interval configured on how often hello logic app will check hello service for an event (up tooevery 15 seconds).</span></span>  

<span data-ttu-id="bd368-124">一旦收到事件時，會引發 hello 邏輯應用程式執行，並開始 hello 工作流程中的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="bd368-124">Once an event is received, hello logic app run will fire and hello actions in hello workflow will start.</span></span>  <span data-ttu-id="bd368-125">您也會無法 tooaccess 整個 hello 工作流程觸發 hello 中的任何資料 （如範例 hello 'On 新推文' 觸發程序會傳入 hello 推文 hello 執行）。</span><span class="sxs-lookup"><span data-stu-id="bd368-125">You will also be able tooaccess any data from hello trigger throughout hello workflow (for example hello 'On a new tweet' trigger will pass hello tweet into hello run).</span></span>

## <a name="actions"></a><span data-ttu-id="bd368-126">動作</span><span class="sxs-lookup"><span data-stu-id="bd368-126">Actions</span></span>
<span data-ttu-id="bd368-127">大部分的連接器會有一個或多個可當做 hello 工作流程的一部分執行的動作。</span><span class="sxs-lookup"><span data-stu-id="bd368-127">Most connectors have one or many actions that can be executed as part of hello workflow.</span></span>  <span data-ttu-id="bd368-128">動作是 hello 執行之後，就可能發生的任何步驟已引發觸發程序。</span><span class="sxs-lookup"><span data-stu-id="bd368-128">Actions are any steps that happen after hello run has fired from a trigger.</span></span>  <span data-ttu-id="bd368-129">tooadd 動作按一下 hello**新步驟**按鈕並搜尋 hello 想 toouse 連接器。</span><span class="sxs-lookup"><span data-stu-id="bd368-129">tooadd an action click hello **New Step** button and search for hello connector you want toouse.</span></span>  <span data-ttu-id="bd368-130">一旦選取 (和之後設定任何[連線](#connections)可能有必要) 您會看到 hello 動作卡，您可以設定。</span><span class="sxs-lookup"><span data-stu-id="bd368-130">Once selected (and after configuring any [connections](#connections) that may be required) you will see hello action card you can configure.</span></span>  <span data-ttu-id="bd368-131">您可以按一下任一 hello 語彙基元的輸出，從上一個步驟中選取資料，或視需要輸入中的任何其他設定。</span><span class="sxs-lookup"><span data-stu-id="bd368-131">You can select data from previous steps by clicking on any of hello tokens for outputs, or enter in any other configuration as needed.</span></span>

![設定連接器動作][2]

## <a name="connections"></a><span data-ttu-id="bd368-133">連線</span><span class="sxs-lookup"><span data-stu-id="bd368-133">Connections</span></span>
<span data-ttu-id="bd368-134">大部分的連接器都需要您 tooconfigure*連接*才能夠使用 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="bd368-134">Most connectors require you tooconfigure a *connection* before you can use hello connector.</span></span>  <span data-ttu-id="bd368-135">A*連接*是任何登入，或需要 tooaccess hello 連接器的連線設定。</span><span class="sxs-lookup"><span data-stu-id="bd368-135">A *connection* is any login or connection configuration needed tooaccess hello connector.</span></span>  <span data-ttu-id="bd368-136">對於使用 OAuth、 建立連接的接點表示登入 hello 服務 （例如 Office 365、 Salesforce 或 GitHub） 可以加密和安全地儲存在 Azure 的密碼存放區存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bd368-136">For connectors that use OAuth, create a connection means signing into hello service (like Office 365, Salesforce, or GitHub) where your access token can be encrypted and securely stored in an Azure secret store.</span></span>  <span data-ttu-id="bd368-137">其他連接器 (例如 FTP 和 SQL) 則需要包含伺服器位址、使用者名稱和密碼等組態的連線。</span><span class="sxs-lookup"><span data-stu-id="bd368-137">Other connectors (like FTP and SQL) require a connection that contains configuration like server address, username, and password.</span></span>  <span data-ttu-id="bd368-138">這些連線的組態詳細資料也會加密並安全地儲存。</span><span class="sxs-lookup"><span data-stu-id="bd368-138">These connection configuration details are also encrypted and securely stored.</span></span>  <span data-ttu-id="bd368-139">連線會無法 tooaccess hello 服務只要 hello 服務允許。</span><span class="sxs-lookup"><span data-stu-id="bd368-139">Connections will be able tooaccess hello service for as long as hello service allows.</span></span>  <span data-ttu-id="bd368-140">Azure Active Directory OAuth 連線 （例如 Office 365 和 Dynamics） 我們可以無限期繼續 toorefresh hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bd368-140">For Azure Active Directory OAuth connections (like Office 365 and Dynamics) we can continue toorefresh hello access token indefinitely.</span></span>  <span data-ttu-id="bd368-141">其他服務則可能會限制權杖的使用時限，在此時限內，完全不需要重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="bd368-141">Other services may put limits on how long we can use a token without it being refreshed.</span></span>  <span data-ttu-id="bd368-142">一般來說，某些動作 (例如變更密碼) 會導致所有存取權杖失效。</span><span class="sxs-lookup"><span data-stu-id="bd368-142">In general certain actions like changing a password will invalidate all access tokens.</span></span>  

<span data-ttu-id="bd368-143">按一下 [瀏覽]，然後選取 [API 連線]，即可在 Azure 中檢視和管理連線。</span><span class="sxs-lookup"><span data-stu-id="bd368-143">Connections can be viewed and managed in Azure by clicking **Browse** and selecting **API Connections**.</span></span>  <span data-ttu-id="bd368-144">從 hello API 連接資源，您可以檢視、 編輯、 更新或重新授權已建立的任何連線。</span><span class="sxs-lookup"><span data-stu-id="bd368-144">From hello API Connections resource you can view, edit, update, or re-authorize any connections you have created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd368-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd368-145">Next Steps</span></span>
* [<span data-ttu-id="bd368-146">建立第一個邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="bd368-146">Create your first logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="bd368-147">了解邏輯應用程式的常見用法和範例</span><span class="sxs-lookup"><span data-stu-id="bd368-147">Learn common uses and examples of logic apps</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="bd368-148">開始使用企業整合觸發程序和動作</span><span class="sxs-lookup"><span data-stu-id="bd368-148">Get started with enterprise integration triggers and actions</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
