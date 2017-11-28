---
title: "在您的 Logic Apps aaaAdd hello Office 365 Outlook 連接器 |Microsoft 文件"
description: "使用 Office 365 連接器 tooenable 互動與 Office 365 中建立邏輯應用程式。 例如：建立、編輯和更新連絡人及行事曆項目。"
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
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="cb1f3-104">開始使用 hello Office 365 Outlook 連接器</span><span class="sxs-lookup"><span data-stu-id="cb1f3-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="cb1f3-105">hello Office 365 Outlook 連接器可讓 Office 365 中 Outlook 的互動。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="cb1f3-106">使用此連接器 toocreate、 編輯和更新連絡人及行事曆項目，以及取得、 傳送，和回覆 tooemail。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="cb1f3-107">使用 Office 365 Outlook，您可以：</span><span class="sxs-lookup"><span data-stu-id="cb1f3-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="cb1f3-108">建置您的工作流程使用 Office 365 中的 hello 電子郵件和行事曆功能。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="cb1f3-109">當新的電子郵件、 行事曆項目更新時，您的工作流程及其他使用觸發程序 toostart。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="cb1f3-110">使用動作 toosend 電子郵件，請建立新的行事曆事件，等等。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="cb1f3-111">例如，當在 Salesforce （觸發程序） 中有新的物件時，傳送電子郵件 tooyour Office 365 Outlook （動作）。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="cb1f3-112">本主題說明您如何 toouse hello 邏輯應用程式中的 Office 365 Outlook 連接器及清單也 hello 觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="cb1f3-113">這個版本的 hello 文件適用於 tooLogic 應用程式公開上市 (GA)。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="cb1f3-114">toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="cb1f3-115">連接 tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="cb1f3-115">Connect tooOffice 365</span></span>
<span data-ttu-id="cb1f3-116">邏輯應用程式可以存取任何服務之前，您先建立*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="cb1f3-117">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="cb1f3-118">例如，tooconnect tooOffice 365 Outlook，您首先需要 Office 365*連接*。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="cb1f3-119">toocreate 連線，請輸入您通常會使用您想要的 tooconnect tooaccess hello 服務的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="cb1f3-120">因此與 Office 365 Outlook，請輸入 hello 認證 tooyour Office 365 帳戶 toocreate hello 連接。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="cb1f3-121">建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="cb1f3-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="cb1f3-122">使用觸發程序</span><span class="sxs-lookup"><span data-stu-id="cb1f3-122">Use a trigger</span></span>
<span data-ttu-id="cb1f3-123">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="cb1f3-124">觸發程序 「 輪詢"hello 服務以間隔和您想要的頻率。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="cb1f3-125">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="cb1f3-126">Hello 邏輯應用程式中，輸入 「 office 365"tooget hello 觸發程序的清單：</span><span class="sxs-lookup"><span data-stu-id="cb1f3-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="cb1f3-127">選取 [Office 365 Outlook - 即將來臨的事件快要開始時]。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="cb1f3-128">如果連接已存在，然後從 hello 下拉式清單選取行事曆。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="cb1f3-129">如果您在提示的 toosign，然後輸入 hello 登詳細資料 toocreate hello 連接中。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="cb1f3-130">[建立 hello 連接](connectors-create-api-office365-outlook.md#create-the-connection)本主題列出 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="cb1f3-131">在此範例中，行事曆事件更新時，會執行 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="cb1f3-132">這個觸發程序，toosee hello 結果加入另一個傳送一則簡訊給您的動作。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="cb1f3-133">例如，新增 hello Twilio*傳送訊息*時 hello 行事曆事件的文字會在 15 分鐘內啟動的動作。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="cb1f3-134">選取 hello**編輯**按鈕，然後設定 hello**頻率**和**間隔**值。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="cb1f3-135">例如，如果您想 hello 觸發程序 toopoll 每隔 15 分鐘，然後設定 hello**頻率**太**分鐘**，並設定 hello**間隔**太**15**.</span><span class="sxs-lookup"><span data-stu-id="cb1f3-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="cb1f3-136">**儲存**您的變更 （hello 工具列的左上的角）。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="cb1f3-137">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="cb1f3-138">使用動作</span><span class="sxs-lookup"><span data-stu-id="cb1f3-138">Use an action</span></span>
<span data-ttu-id="cb1f3-139">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="cb1f3-140">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="cb1f3-141">選取加號 hello。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-141">Select hello plus sign.</span></span> <span data-ttu-id="cb1f3-142">您會看到幾個選擇：**將動作加入**，**加入條件**，或其中一個 hello**詳細**選項。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="cb1f3-143">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="cb1f3-144">在 [hello] 文字方塊中，輸入 「 office 365"tooget 所有 hello 可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="cb1f3-145">在本例中，選擇 [Office 365 Outlook - 建立連絡人]。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="cb1f3-146">如果連接已存在，然後選擇 hello**資料夾識別碼**，**名字**，和其他屬性：</span><span class="sxs-lookup"><span data-stu-id="cb1f3-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="cb1f3-147">如果系統提示您輸入 hello 連接資訊，然後輸入 hello 詳細資料 toocreate hello 連接。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="cb1f3-148">[建立 hello 連接](connectors-create-api-office365-outlook.md#create-the-connection)本主題說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="cb1f3-149">在此範例中，我們會在 Office 365 Outlook 中建立新連絡人。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="cb1f3-150">您可以使用另一個觸發程序 toocreate hello 連絡人的輸出。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="cb1f3-151">例如，新增 hello SalesForce*當建立物件*觸發程序。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="cb1f3-152">然後新增 Office 365 Outlook hello*建立連絡人*動作若使用 hello SalesForce 欄位 toocreate hello 新增新的連絡人 Office 365 中。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="cb1f3-153">**儲存**您的變更 （hello 工具列的左上的角）。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="cb1f3-154">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="cb1f3-155">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="cb1f3-155">Connector-specific details</span></span>

<span data-ttu-id="cb1f3-156">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/office365connector/)。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cb1f3-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb1f3-157">Next Steps</span></span>
<span data-ttu-id="cb1f3-158">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="cb1f3-159">瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1f3-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

