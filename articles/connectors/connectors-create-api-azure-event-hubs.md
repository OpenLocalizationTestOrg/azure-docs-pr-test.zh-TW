---
title: "使用 Azure 事件中樞為 Azure Logic Apps 設定事件監視器 | Microsoft Docs"
description: "使用 Azure 事件中樞來監視資料流，為 Azure Logic Apps 接收事件和傳送事件"
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
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="eddc9-104">使用事件中樞連接器來監視、接收及傳送事件</span><span class="sxs-lookup"><span data-stu-id="eddc9-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="eddc9-105">若要設定事件監視器，以便邏輯應用程式偵測事件、接收事件和傳送事件，請從您的邏輯應用程式連線到 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs)。</span><span class="sxs-lookup"><span data-stu-id="eddc9-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="eddc9-106">深入了解 [Azure 事件中樞](../event-hubs/event-hubs-what-is-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="eddc9-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="eddc9-107">需求</span><span class="sxs-lookup"><span data-stu-id="eddc9-107">Requirements</span></span>

* <span data-ttu-id="eddc9-108">您在 Azure 中必須有[事件中樞命名空間和事件中樞](../event-hubs/event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="eddc9-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="eddc9-109">了解[如何建立事件中樞命名空間和事件中樞](../event-hubs/event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="eddc9-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="eddc9-110">若要在邏輯應用程式中使用[任何連接器](https://docs.microsoft.com/azure/connectors/apis-list)，您必須先建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="eddc9-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="eddc9-111">了解[如何建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="eddc9-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="eddc9-112">檢查事件中樞命名空間權限並尋找連接字串</span><span class="sxs-lookup"><span data-stu-id="eddc9-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="eddc9-113">若要讓邏輯應用程式存取任何服務，您必須建立邏輯應用程式與服務之間的[*連線*](./connectors-overview.md)(如果您還尚未這麼做)。</span><span class="sxs-lookup"><span data-stu-id="eddc9-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="eddc9-114">此連線會授權邏輯應用程式存取資料。</span><span class="sxs-lookup"><span data-stu-id="eddc9-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="eddc9-115">若要讓邏輯應用程式存取事件中樞，您必須擁有事件中樞命名空間的 [管理] 權限和連接字串。</span><span class="sxs-lookup"><span data-stu-id="eddc9-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="eddc9-116">若要檢查您的權限並取得連接字串，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="eddc9-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="eddc9-117">登入 [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="eddc9-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="eddc9-118">移至您的事件中樞「命名空間」，而不是特定事件中樞。</span><span class="sxs-lookup"><span data-stu-id="eddc9-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="eddc9-119">在命名空間刀鋒視窗的 [設定] 之下，選擇 [共用存取原則]。</span><span class="sxs-lookup"><span data-stu-id="eddc9-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="eddc9-120">在 [宣告] 之下，確認您有該命名空間的 [管理] 權限。</span><span class="sxs-lookup"><span data-stu-id="eddc9-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![管理事件中樞命名空間的權限](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="eddc9-122">若要複製事件中樞命名空間的連接字串，請選擇 [RootManageSharedAccessKey]。</span><span class="sxs-lookup"><span data-stu-id="eddc9-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="eddc9-123">選擇您的主索引鍵連接字串旁邊的 [複製] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eddc9-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![複製事件中樞命名空間連接字串](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="eddc9-125">若要確認您的連接字串是否與您的事件中樞命名空間或特定事件中樞相關聯，請檢查連接字串中的 `EntityPath` 參數。</span><span class="sxs-lookup"><span data-stu-id="eddc9-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="eddc9-126">如果您發現這個參數，此連接字串適用於特定事件中樞「實體」，而不是使用您的邏輯應用程式的正確字串。</span><span class="sxs-lookup"><span data-stu-id="eddc9-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="eddc9-127">將事件中樞觸發程序或動作新增至邏輯應用程式之後，當系統提示您輸入認證時，您可以連線至您的事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="eddc9-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="eddc9-128">指定您的連線名稱，輸入您複製的連接字串，然後選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="eddc9-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![輸入事件中樞命名空間的連接字串](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="eddc9-130">您在建立連線之後，連線名稱應該會出現在事件中樞觸發程序或動作中。</span><span class="sxs-lookup"><span data-stu-id="eddc9-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="eddc9-131">您現在可以在您的邏輯應用程式中繼續進行其他步驟。</span><span class="sxs-lookup"><span data-stu-id="eddc9-131">You can then continue with the other steps in your logic app.</span></span>

    ![已建立事件中樞命名空間連線](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="eddc9-133">在事件中樞收到新事件時啟動工作流程</span><span class="sxs-lookup"><span data-stu-id="eddc9-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="eddc9-134">[觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)是在邏輯應用程式中啟動工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="eddc9-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="eddc9-135">若要在新事件傳送至事件中樞時啟動工作流程，請遵循下列步驟來新增可偵測此事件的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="eddc9-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="eddc9-136">在 [Azure 入口網站](https://portal.azure.com "Azure 入口網站")中，移至現有的邏輯應用程式，或建立空白的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="eddc9-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="eddc9-137">在邏輯應用程式設計工具的搜尋方塊中，輸入 `event hubs` 作為您的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="eddc9-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="eddc9-138">選取此觸發程序︰**當事件可用於事件中樞時**</span><span class="sxs-lookup"><span data-stu-id="eddc9-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![選取當事件中樞收到新事件時的觸發程序](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="eddc9-140">如果您還沒有事件中樞命名空間的連線，系統會提示您立即建立此連線。</span><span class="sxs-lookup"><span data-stu-id="eddc9-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="eddc9-141">指定您的連線名稱，然後輸入事件中樞命名空間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="eddc9-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="eddc9-142">如有必要，請了解[如何尋找您的連接字串](#permissions-connection-string)。</span><span class="sxs-lookup"><span data-stu-id="eddc9-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![輸入事件中樞命名空間的連接字串](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="eddc9-144">在您建立連線之後，[當事件可用於事件中樞時] 觸發程序的設定隨即出現。</span><span class="sxs-lookup"><span data-stu-id="eddc9-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![當事件中樞收到新事件時的觸發程序設定](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="eddc9-146">輸入或選取您想要監視的事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="eddc9-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="eddc9-147">選取您想要檢查事件中樞的頻率和間隔。</span><span class="sxs-lookup"><span data-stu-id="eddc9-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="eddc9-148">若要選擇性地選取取用者群組以便讀取事件，請選擇 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="eddc9-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![指定事件中樞或取用者群組](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="eddc9-150">您現在已設定觸發程序以啟動邏輯應用程式的工作流程。</span><span class="sxs-lookup"><span data-stu-id="eddc9-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="eddc9-151">您的邏輯應用程式會根據您所設定的排程，檢查指定的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="eddc9-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="eddc9-152">如果您的應用程式在事件中樞找到新的事件，觸發程序就會在邏輯應用程式中執行其他動作或觸發程序。</span><span class="sxs-lookup"><span data-stu-id="eddc9-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="eddc9-153">將事件從邏輯應用程式傳送至事件中樞</span><span class="sxs-lookup"><span data-stu-id="eddc9-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="eddc9-154">[動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)是邏輯應用程式工作流程所執行的工作。</span><span class="sxs-lookup"><span data-stu-id="eddc9-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="eddc9-155">將觸發程序新增至邏輯應用程式之後，您可以新增一個動作，以對該觸發程序所產生的資料執行作業。</span><span class="sxs-lookup"><span data-stu-id="eddc9-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="eddc9-156">若要將事件從邏輯應用程式傳送至事件中樞，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="eddc9-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="eddc9-157">在邏輯應用程式設計工具中，於您的邏輯應用程式觸發程序之下，選擇 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="eddc9-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![選擇 [新增步驟]，然後選擇 [新增動作]](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="eddc9-159">您現在可以尋找並選取要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="eddc9-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="eddc9-160">雖然您可以選取任何動作，但在這個範例中，我們希望事件中樞動作傳送事件。</span><span class="sxs-lookup"><span data-stu-id="eddc9-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="eddc9-161">在搜尋方塊中，輸入 `event hubs` 作為篩選條件。</span><span class="sxs-lookup"><span data-stu-id="eddc9-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="eddc9-162">選取此動作︰**傳送事件**</span><span class="sxs-lookup"><span data-stu-id="eddc9-162">Select this action: **Send event**</span></span>

    ![選取「事件中樞 - 傳送事件」動作](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="eddc9-164">輸入事件的必要詳細資料，例如要傳送事件的事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="eddc9-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="eddc9-165">輸入有關事件的其他任何選擇性詳細資料，例如該事件的內容。</span><span class="sxs-lookup"><span data-stu-id="eddc9-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="eddc9-166">若要選擇性地指定要傳送事件的事件中樞資料分割，請選擇 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="eddc9-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![輸入事件中樞名稱和選擇性事件詳細資料](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="eddc9-168">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="eddc9-168">Save your changes.</span></span>

    ![儲存您的邏輯應用程式](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="eddc9-170">您現在已設定可從邏輯應用程式傳送事件的動作。</span><span class="sxs-lookup"><span data-stu-id="eddc9-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="eddc9-171">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="eddc9-171">Connector-specific details</span></span>

<span data-ttu-id="eddc9-172">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/eventhubs/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="eddc9-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="eddc9-173">取得說明</span><span class="sxs-lookup"><span data-stu-id="eddc9-173">Get help</span></span>

<span data-ttu-id="eddc9-174">若要提出問題、回答問題以及查看其他 Azure Logic Apps 使用者的做法，請造訪 [Azure Logic Apps 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="eddc9-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="eddc9-175">若要改善 Logic Apps 和連接器，請在 [Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)上票選或提交想法。</span><span class="sxs-lookup"><span data-stu-id="eddc9-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eddc9-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eddc9-176">Next steps</span></span>

*  [<span data-ttu-id="eddc9-177">尋找 Azure Logic Apps 的其他連接器</span><span class="sxs-lookup"><span data-stu-id="eddc9-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)