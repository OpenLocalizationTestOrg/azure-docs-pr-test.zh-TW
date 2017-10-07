---
title: "總為 Azure 邏輯應用程式的 Azure 事件中心的事件監視 aaaSet |Microsoft 文件"
description: "監視資料的資料流 tooreceive 事件和事件傳送為 Azure 事件中心的 Azure 邏輯應用程式"
services: logic-apps
keywords: "資料流、事件監視器、事件中樞"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="7a6f1-104">監視、 接收和傳送與 hello 事件中心連接器事件</span><span class="sxs-lookup"><span data-stu-id="7a6f1-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="7a6f1-105">tooset 總事件監視，因此邏輯應用程式可以偵測事件，會接收事件，且事件，傳送連接 tooan [Azure 事件中心](https://azure.microsoft.com/services/event-hubs)從邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="7a6f1-106">深入了解 [Azure 事件中樞](../event-hubs/event-hubs-what-is-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="7a6f1-107">需求</span><span class="sxs-lookup"><span data-stu-id="7a6f1-107">Requirements</span></span>

* <span data-ttu-id="7a6f1-108">您有 toohave[事件中樞命名空間和事件中心](../event-hubs/event-hubs-create.md)在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="7a6f1-109">深入了解[如何 toocreate 事件中樞命名空間和事件中心](../event-hubs/event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="7a6f1-110">toouse[任何連接器](https://docs.microsoft.com/azure/connectors/apis-list)在邏輯應用程式，您必須 toocreate 邏輯應用程式第一次。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="7a6f1-111">深入了解[如何 toocreate 邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="7a6f1-112">檢查事件中樞命名空間的權限，並尋找 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="7a6f1-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="7a6f1-113">如您邏輯應用程式 tooaccess 任何服務，您有 toocreate [*連接*](./connectors-overview.md)之間邏輯應用程式與 hello 服務，如果您還沒有這麼做。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="7a6f1-114">此連接會授權您 tooaccess 邏輯應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="7a6f1-115">您的邏輯應用程式 tooaccess 事件中樞，您必須 toohave**管理**權限和 hello 事件中樞命名空間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="7a6f1-116">toocheck 您權限和 get hello 連接字串，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="7a6f1-117">登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="7a6f1-118">移 tooyour 事件中心*命名空間*，不 hello 特定事件中心。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="7a6f1-119">Hello 命名空間 刀鋒視窗底下**設定**，選擇**共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="7a6f1-120">在 [宣告] 之下，確認您有該命名空間的 [管理] 權限。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![管理事件中樞命名空間的權限](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="7a6f1-122">toocopy hello 連接字串 hello 事件中樞命名空間中，選擇**RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="7a6f1-123">下一步 tooyour 主索引鍵的連接字串中，選擇 hello 複製 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![複製事件中樞命名空間連接字串](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="7a6f1-125">tooconfirm 與事件中樞命名空間或特定的事件中心，相關聯的連接字串是否檢查 hello 連接字串 hello`EntityPath`參數。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="7a6f1-126">如果您發現此參數，hello 連接字串是特定的事件中心 「 實體 」，而非 hello 正確的字串 toouse 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="7a6f1-127">現在當系統提示您輸入認證加入事件中心觸發程序或動作 tooyour 邏輯應用程式之後，您可以連接 tooyour 事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="7a6f1-128">為您的連線指定名稱，輸入 hello 連接字串，複製，再選擇**建立**。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![輸入事件中樞命名空間的連接字串](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="7a6f1-130">建立您的連線之後，hello 連接名稱應該會出現在 hello 事件中心觸發程序或動作。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="7a6f1-131">然後，您可以繼續使用 hello 邏輯應用程式中的其他步驟。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-131">You can then continue with hello other steps in your logic app.</span></span>

    ![已建立事件中樞命名空間連線](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="7a6f1-133">在事件中樞收到新事件時啟動工作流程</span><span class="sxs-lookup"><span data-stu-id="7a6f1-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="7a6f1-134">[觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)是在邏輯應用程式中啟動工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="7a6f1-135">新的事件傳送 tooyour 事件中樞時，請啟動的工作流程，請遵循下列步驟來新增 hello 觸發程序偵測到此事件。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="7a6f1-136">在 hello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")、 移 tooyour 現有邏輯應用程式，或建立空白的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="7a6f1-137">在 hello hello 邏輯應用程式的設計工具搜尋方塊中輸入`event hubs`用於您篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="7a6f1-138">選取此觸發程序︰**當事件可用於事件中樞時**</span><span class="sxs-lookup"><span data-stu-id="7a6f1-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![選取當事件中樞收到新事件時的觸發程序](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="7a6f1-140">如果您還沒有連接 tooyour 事件中樞命名空間，則會提示您 toocreate 現在這個連線。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="7a6f1-141">指定的名稱，您的連線，並輸入您的事件中樞命名空間 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="7a6f1-142">如有必要，了解[如何 toofind 連接字串](#permissions-connection-string)。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![輸入事件中樞命名空間的連接字串](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="7a6f1-144">建立 hello 連線之後，hello 設定 hello**內發生事件時使用事件中心**觸發程序會出現。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![當事件中樞收到新事件時的觸發程序設定](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="7a6f1-146">輸入或選取 hello hello 想 toomonitor 事件中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="7a6f1-147">選取 hello 頻率和間隔 toocheck hello 事件中心的頻率。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="7a6f1-148">toooptionally 選取讀取事件的取用者群組中，選擇  **Show advanced 選項**。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![指定事件中樞或取用者群組](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="7a6f1-150">您現在設定觸發程序 toostart 工作流程應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="7a6f1-151">應用程式邏輯會檢查 hello 指定根據您設定的 hello 排程的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="7a6f1-152">如果您的應用程式中 hello 事件中心，找到新的事件，hello 觸發程序，則會執行其他動作或觸發程序邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="7a6f1-153">從邏輯應用程式傳送事件 tooyour 事件中樞</span><span class="sxs-lookup"><span data-stu-id="7a6f1-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="7a6f1-154">[動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)是邏輯應用程式工作流程所執行的工作。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="7a6f1-155">新增觸發程序 tooyour 邏輯應用程式之後，您可以加入動作 tooperform 操作該觸發程序所產生的資料。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="7a6f1-156">toosend 事件 tooyour 事件中心從邏輯應用程式，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="7a6f1-157">在邏輯應用程式設計工具中，於您的邏輯應用程式觸發程序之下，選擇 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![選擇 [新增步驟]，然後選擇 [新增動作]](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="7a6f1-159">現在您可以尋找並選取動作 tooperform。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="7a6f1-160">雖然您可以選取任何動作，如這個範例中，我們想要 hello 事件中心動作 toosend 事件。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="7a6f1-161">在 [hello] 搜尋方塊中，輸入`event hubs`用於您篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="7a6f1-162">選取此動作︰**傳送事件**</span><span class="sxs-lookup"><span data-stu-id="7a6f1-162">Select this action: **Send event**</span></span>

    ![選取「事件中樞 - 傳送事件」動作](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="7a6f1-164">Hello 事件，例如 hello hello 想 toosend hello 事件的事件中樞的名稱，請輸入所需的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="7a6f1-165">輸入任何其他選擇性 hello 事件，例如，針對該事件內容的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="7a6f1-166">toooptionally 指定 hello 事件中心資料分割，其中 toosend hello 事件，選擇**Show advanced 選項**。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![輸入事件中樞名稱和選擇性事件詳細資料](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="7a6f1-168">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-168">Save your changes.</span></span>

    ![儲存您的邏輯應用程式](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="7a6f1-170">您現在已設定動作 toosend 事件，從應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="7a6f1-171">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="7a6f1-171">Connector-specific details</span></span>

<span data-ttu-id="7a6f1-172">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/eventhubs/)。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="7a6f1-173">取得說明</span><span class="sxs-lookup"><span data-stu-id="7a6f1-173">Get help</span></span>

<span data-ttu-id="7a6f1-174">tooask 問題、 解答的問題，以及執行其他 Azure 邏輯應用程式使用者，請參閱瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="7a6f1-175">toohelp 改善邏輯應用程式和連接器、 票選或送出意見在 hello [Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)。</span><span class="sxs-lookup"><span data-stu-id="7a6f1-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a6f1-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a6f1-176">Next steps</span></span>

*  [<span data-ttu-id="7a6f1-177">尋找 Azure Logic Apps 的其他連接器</span><span class="sxs-lookup"><span data-stu-id="7a6f1-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)