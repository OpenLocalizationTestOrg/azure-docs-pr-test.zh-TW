---
title: "在您的 Logic Apps 中新增 OneDrive 連接器 | Microsoft Docs"
description: "搭配 REST API 參數來使用 OneDrive 連接器的概觀"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="0814a-103">開始使用 OneDrive 連接器</span><span class="sxs-lookup"><span data-stu-id="0814a-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="0814a-104">連線到 OneDrive 來管理您的檔案，包括上傳檔案、取得、刪除檔案等等。</span><span class="sxs-lookup"><span data-stu-id="0814a-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="0814a-105">使用 OneDrive，您會︰</span><span class="sxs-lookup"><span data-stu-id="0814a-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="0814a-106">將檔案儲存在 OneDrive 中或更新 OneDrive 中的現有檔案以建置您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="0814a-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="0814a-107">使用觸發程序，在 OneDrive 內有檔案建立或更新時，啟動工作流程。</span><span class="sxs-lookup"><span data-stu-id="0814a-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="0814a-108">使用動作來建立檔案、刪除檔案等等。</span><span class="sxs-lookup"><span data-stu-id="0814a-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="0814a-109">例如，當收到有附件的新 Office 365 電子郵件時 (觸發程序)，在 OneDrive 建立新的檔案 (動作)。</span><span class="sxs-lookup"><span data-stu-id="0814a-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="0814a-110">本主題說明如何在邏輯應用程式中使用 OneDrive 連接器，並且也列出觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="0814a-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="0814a-111">若要深入瞭解 Logic Apps，請參閱[什麼是邏輯應用程式](../logic-apps/logic-apps-what-are-logic-apps.md)以及[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="0814a-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="0814a-112">連線到 OneDrive</span><span class="sxs-lookup"><span data-stu-id="0814a-112">Connect to OneDrive</span></span>
<span data-ttu-id="0814a-113">您必須先建立與服務的「連線」，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="0814a-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="0814a-114">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="0814a-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="0814a-115">例如，若要連線到 OneDrive，您必須先有 OneDrive「連線」。</span><span class="sxs-lookup"><span data-stu-id="0814a-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="0814a-116">若要建立連線，請輸入平常用來存取所要連線之服務的認證。</span><span class="sxs-lookup"><span data-stu-id="0814a-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="0814a-117">因此，在 OneDrive 中，請在 OneDrive 帳戶輸入認證以建立連線。</span><span class="sxs-lookup"><span data-stu-id="0814a-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="0814a-118">建立連線</span><span class="sxs-lookup"><span data-stu-id="0814a-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="0814a-119">使用觸發程序</span><span class="sxs-lookup"><span data-stu-id="0814a-119">Use a trigger</span></span>
<span data-ttu-id="0814a-120">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="0814a-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="0814a-121">觸發程序會以您想要的間隔和頻率「輪詢」服務。</span><span class="sxs-lookup"><span data-stu-id="0814a-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="0814a-122">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="0814a-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="0814a-123">在邏輯應用程式中，輸入「onedrive」以取得觸發程序的清單︰</span><span class="sxs-lookup"><span data-stu-id="0814a-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="0814a-124">選取 [當檔案遭到修改時]。</span><span class="sxs-lookup"><span data-stu-id="0814a-124">Select **When a file is modified**.</span></span> <span data-ttu-id="0814a-125">如果連線已存在，則選取 [顯示選擇器] 按鈕以選取資料夾。</span><span class="sxs-lookup"><span data-stu-id="0814a-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="0814a-126">如果系統提示您登入，則輸入登入詳細資料來建立連線。</span><span class="sxs-lookup"><span data-stu-id="0814a-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="0814a-127">本主題中的[建立連線](connectors-create-api-onedrive.md#create-the-connection)一節會列出步驟。</span><span class="sxs-lookup"><span data-stu-id="0814a-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0814a-128">在此範例中，當所選資料夾中的檔案更新時，邏輯應用程式便會執行。</span><span class="sxs-lookup"><span data-stu-id="0814a-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="0814a-129">若要查看此觸發程序的結果，請新增另一個動作，以傳送電子郵件給您。</span><span class="sxs-lookup"><span data-stu-id="0814a-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="0814a-130">例如，新增 Office 365 Outlook「傳送電子郵件」動作，以在檔案更新時傳送電子郵件給您。</span><span class="sxs-lookup"><span data-stu-id="0814a-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="0814a-131">選取 [編輯] 按鈕，然後設定 [頻率] 和 [間隔] 值。</span><span class="sxs-lookup"><span data-stu-id="0814a-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="0814a-132">例如，如果您希望觸發程序每隔 15 分鐘輪詢一次，則將 [頻率] 設定為 [分鐘] 並將 [間隔] 設定為 [15]。</span><span class="sxs-lookup"><span data-stu-id="0814a-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="0814a-133">**儲存**您的變更 (工具列的左上角)。</span><span class="sxs-lookup"><span data-stu-id="0814a-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="0814a-134">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="0814a-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="0814a-135">使用動作</span><span class="sxs-lookup"><span data-stu-id="0814a-135">Use an action</span></span>
<span data-ttu-id="0814a-136">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="0814a-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="0814a-137">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="0814a-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="0814a-138">選取加號。</span><span class="sxs-lookup"><span data-stu-id="0814a-138">Select the plus sign.</span></span> <span data-ttu-id="0814a-139">您會看到幾個選擇︰[新增動作]、[新增條件] 或其中一個 [其他] 選項。</span><span class="sxs-lookup"><span data-stu-id="0814a-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="0814a-140">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="0814a-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="0814a-141">在文字方塊中，輸入「onedrive」以取得所有可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="0814a-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="0814a-142">在我們的範例中，選擇 [OneDrive - 建立檔案]。</span><span class="sxs-lookup"><span data-stu-id="0814a-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="0814a-143">如果連線已存在，則選取 [資料夾路徑] 以供放置檔案、輸入 [檔案名稱]，然後選擇想要的 [檔案內容]︰</span><span class="sxs-lookup"><span data-stu-id="0814a-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="0814a-144">如果系統提示您輸入連線資訊，請輸入詳細資料以建立連線。</span><span class="sxs-lookup"><span data-stu-id="0814a-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="0814a-145">本主題的[建立連線](connectors-create-api-onedrive.md#create-the-connection)一節會說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="0814a-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0814a-146">在此範例中，我們會在 OneDrive 資料夾建立新檔案。</span><span class="sxs-lookup"><span data-stu-id="0814a-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="0814a-147">您可以使用另一個觸發程序的輸出以建立 OneDrive 檔案。</span><span class="sxs-lookup"><span data-stu-id="0814a-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="0814a-148">例如，新增 Office 365 Outlook「新的電子郵件送達時」觸發程序。</span><span class="sxs-lookup"><span data-stu-id="0814a-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="0814a-149">然後新增 OneDrive「建立檔案」動作，使用 ForEach 內的 [附件] 和 [內容類型] 欄位在 OneDrive 中建立新檔案。</span><span class="sxs-lookup"><span data-stu-id="0814a-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="0814a-150">**儲存**您的變更 (工具列的左上角)。</span><span class="sxs-lookup"><span data-stu-id="0814a-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="0814a-151">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="0814a-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="0814a-152">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="0814a-152">Connector-specific details</span></span>

<span data-ttu-id="0814a-153">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/onedriveconnector/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="0814a-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="0814a-154">其他連接器</span><span class="sxs-lookup"><span data-stu-id="0814a-154">More connectors</span></span>
<span data-ttu-id="0814a-155">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="0814a-155">Go back to the [APIs list](apis-list.md).</span></span>