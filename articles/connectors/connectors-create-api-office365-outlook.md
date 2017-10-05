---
title: "在您的 Logic Apps 中新增 Office 365 Outlook 連接器 | Microsoft Docs"
description: "建立具有 Office 365 連接器的邏輯應用程式來啟用與 Office 365 的互動。 例如：建立、編輯和更新連絡人及行事曆項目。"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 5335dae62e61659b68e8befb4ed0d404dffb800c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-outlook-connector"></a><span data-ttu-id="57fdf-104">開始使用 Office 365 Outlook 連接器</span><span class="sxs-lookup"><span data-stu-id="57fdf-104">Get started with the Office 365 Outlook connector</span></span>
<span data-ttu-id="57fdf-105">Office 365 Outlook 連接器能夠與 Office 365 中的 Outlook 互動。</span><span class="sxs-lookup"><span data-stu-id="57fdf-105">The Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="57fdf-106">使用此連接器來建立、編輯和更新連絡人和行事曆項目，也可取得、傳送及回覆電子郵件。</span><span class="sxs-lookup"><span data-stu-id="57fdf-106">Use this connector to create, edit, and update contacts and calendar items, and also get, send, and reply to email.</span></span>

<span data-ttu-id="57fdf-107">使用 Office 365 Outlook，您可以：</span><span class="sxs-lookup"><span data-stu-id="57fdf-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="57fdf-108">使用 Office 365 中的電子郵件和行事曆功能來建置您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="57fdf-108">Build your workflow using the email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="57fdf-109">使用觸發程序，在有新的電子郵件時、行事曆項目更新時等情況啟動您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="57fdf-109">Use triggers to start your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="57fdf-110">使用傳送電子郵件、建立新的行事曆事件等等的動作。</span><span class="sxs-lookup"><span data-stu-id="57fdf-110">Use actions to send an email, create a new calendar event, and more.</span></span> <span data-ttu-id="57fdf-111">例如，當 Salesforce 中有新的物件時，傳送電子郵件給您的 Office 365 Outlook (動作)。</span><span class="sxs-lookup"><span data-stu-id="57fdf-111">For example, when there is a new object in Salesforce (a trigger), send an email to your Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="57fdf-112">本主題說明如何在邏輯應用程式中使用 Office 365 Outlook 連接器，並且也列出觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="57fdf-112">This topic shows you how to use the Office 365 Outlook connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="57fdf-113">這個版本的文章適用於 Logic Apps 公開上市版本 (GA)。</span><span class="sxs-lookup"><span data-stu-id="57fdf-113">This version of the article applies to Logic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="57fdf-114">若要深入瞭解 Logic Apps，請參閱[什麼是邏輯應用程式](../logic-apps/logic-apps-what-are-logic-apps.md)以及[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="57fdf-114">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="57fdf-115">連接至 Office 365</span><span class="sxs-lookup"><span data-stu-id="57fdf-115">Connect to Office 365</span></span>
<span data-ttu-id="57fdf-116">您必須先建立與服務的「連線」，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="57fdf-116">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="57fdf-117">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="57fdf-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="57fdf-118">例如，若要連線到 Office 365 Outlook，您必須先有 Office 365「連線」。</span><span class="sxs-lookup"><span data-stu-id="57fdf-118">For example, to connect to Office 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="57fdf-119">若要建立連線，請輸入平常用來存取所要連線之服務的認證。</span><span class="sxs-lookup"><span data-stu-id="57fdf-119">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="57fdf-120">因此，在 Office 365 Outlook 中，請在 Office 365 帳戶輸入認證以建立連線。</span><span class="sxs-lookup"><span data-stu-id="57fdf-120">So with Office 365 Outlook, enter the credentials to your Office 365 account to create the connection.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="57fdf-121">建立連線</span><span class="sxs-lookup"><span data-stu-id="57fdf-121">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to Office 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="57fdf-122">使用觸發程序</span><span class="sxs-lookup"><span data-stu-id="57fdf-122">Use a trigger</span></span>
<span data-ttu-id="57fdf-123">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="57fdf-123">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="57fdf-124">觸發程序會以您想要的間隔和頻率「輪詢」服務。</span><span class="sxs-lookup"><span data-stu-id="57fdf-124">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="57fdf-125">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="57fdf-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="57fdf-126">在邏輯應用程式中，輸入 "office 365" 以取得觸發程序的清單︰</span><span class="sxs-lookup"><span data-stu-id="57fdf-126">In the logic app, type "office 365" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="57fdf-127">選取 [Office 365 Outlook - 即將來臨的事件快要開始時]。</span><span class="sxs-lookup"><span data-stu-id="57fdf-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="57fdf-128">如果連線已存在，則選取下拉式清單中的行事曆。</span><span class="sxs-lookup"><span data-stu-id="57fdf-128">If a connection already exists, then select a calendar from the drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="57fdf-129">如果系統提示您登入，則輸入登入詳細資料來建立連線。</span><span class="sxs-lookup"><span data-stu-id="57fdf-129">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="57fdf-130">本主題中的[建立連線](connectors-create-api-office365-outlook.md#create-the-connection)一節會列出步驟。</span><span class="sxs-lookup"><span data-stu-id="57fdf-130">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="57fdf-131">在此範例中，邏輯應用程式會在行事曆事件更新時執行。</span><span class="sxs-lookup"><span data-stu-id="57fdf-131">In this example, the logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="57fdf-132">若要查看此觸發程序的結果，請新增另一個動作，以傳送簡訊給您。</span><span class="sxs-lookup"><span data-stu-id="57fdf-132">To see the results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="57fdf-133">例如，加入 Twilio「傳送訊息」動作，以便在行事曆事件於 15 分鐘內開始時傳送簡訊給您。</span><span class="sxs-lookup"><span data-stu-id="57fdf-133">For example, add the Twilio *Send message* action that texts you when the calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="57fdf-134">選取 [編輯] 按鈕，然後設定 [頻率] 和 [間隔] 值。</span><span class="sxs-lookup"><span data-stu-id="57fdf-134">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="57fdf-135">例如，如果您希望觸發程序每隔 15 分鐘輪詢一次，則將 [頻率] 設定為 [分鐘] 並將 [間隔] 設定為 [15]。</span><span class="sxs-lookup"><span data-stu-id="57fdf-135">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="57fdf-136">**儲存**您的變更 (工具列的左上角)。</span><span class="sxs-lookup"><span data-stu-id="57fdf-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="57fdf-137">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="57fdf-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="57fdf-138">使用動作</span><span class="sxs-lookup"><span data-stu-id="57fdf-138">Use an action</span></span>
<span data-ttu-id="57fdf-139">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="57fdf-139">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="57fdf-140">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="57fdf-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="57fdf-141">選取加號。</span><span class="sxs-lookup"><span data-stu-id="57fdf-141">Select the plus sign.</span></span> <span data-ttu-id="57fdf-142">您會看到幾個選擇︰[新增動作]、[新增條件] 或其中一個 [其他] 選項。</span><span class="sxs-lookup"><span data-stu-id="57fdf-142">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="57fdf-143">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="57fdf-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="57fdf-144">在文字方塊中，輸入 “office 365” 以取得所有可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="57fdf-144">In the text box, type “office 365” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="57fdf-145">在本例中，選擇 [Office 365 Outlook - 建立連絡人]。</span><span class="sxs-lookup"><span data-stu-id="57fdf-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="57fdf-146">如果連線已存在，則選擇 [資料夾識別碼]、[名字] 和其他屬性︰</span><span class="sxs-lookup"><span data-stu-id="57fdf-146">If a connection already exists, then choose the **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="57fdf-147">如果系統提示您輸入連線資訊，請輸入詳細資料以建立連線。</span><span class="sxs-lookup"><span data-stu-id="57fdf-147">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="57fdf-148">本主題的[建立連線](connectors-create-api-office365-outlook.md#create-the-connection)一節會說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="57fdf-148">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="57fdf-149">在此範例中，我們會在 Office 365 Outlook 中建立新連絡人。</span><span class="sxs-lookup"><span data-stu-id="57fdf-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="57fdf-150">您可以使用另一個觸發程序的輸出來建立連絡人。</span><span class="sxs-lookup"><span data-stu-id="57fdf-150">You can use output from another trigger to create the contact.</span></span> <span data-ttu-id="57fdf-151">例如，新增 SalesForce「當物件建立時」觸發程序。</span><span class="sxs-lookup"><span data-stu-id="57fdf-151">For example, add the SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="57fdf-152">然後新增 Office 365 Outlook「建立連絡人」動作，以使用 SalesForce 欄位在 Office 365 中建立新的新連絡人。</span><span class="sxs-lookup"><span data-stu-id="57fdf-152">Then add the Office 365 Outlook *Create contact* action that uses the SalesForce fields to create the new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="57fdf-153">**儲存**您的變更 (工具列的左上角)。</span><span class="sxs-lookup"><span data-stu-id="57fdf-153">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="57fdf-154">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="57fdf-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="57fdf-155">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="57fdf-155">Connector-specific details</span></span>

<span data-ttu-id="57fdf-156">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/office365connector/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="57fdf-156">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="57fdf-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57fdf-157">Next Steps</span></span>
<span data-ttu-id="57fdf-158">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="57fdf-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="57fdf-159">請到我們的 [API 清單](apis-list.md)探索 Logic Apps 中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="57fdf-159">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

