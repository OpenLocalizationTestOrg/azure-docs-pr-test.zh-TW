---
title: "在您的 Logic Apps aaaAdd hello OneDrive 連接器 |Microsoft 文件"
description: "使用 REST API 參數 hello OneDrive 連接器概觀"
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
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="f587e-103">開始使用 hello OneDrive 連接器</span><span class="sxs-lookup"><span data-stu-id="f587e-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="f587e-104">連接 tooOneDrive toomanage 檔案，包括上傳、 get、 刪除檔案等等。</span><span class="sxs-lookup"><span data-stu-id="f587e-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="f587e-105">使用 OneDrive，您會︰</span><span class="sxs-lookup"><span data-stu-id="f587e-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="f587e-106">將檔案儲存在 OneDrive 中或更新 OneDrive 中的現有檔案以建置您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="f587e-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="f587e-107">建立或更新您的 OneDrive 中的檔案時使用觸發程序 toostart 您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="f587e-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="f587e-108">使用動作 toocreate 檔案，請刪除檔案，等等。</span><span class="sxs-lookup"><span data-stu-id="f587e-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="f587e-109">例如，當收到有附件的新 Office 365 電子郵件時 (觸發程序)，在 OneDrive 建立新的檔案 (動作)。</span><span class="sxs-lookup"><span data-stu-id="f587e-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="f587e-110">本主題說明您如何 toouse hello 邏輯應用程式中的 OneDrive 連接器及清單也 hello 觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="f587e-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="f587e-111">toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f587e-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="f587e-112">連接 tooOneDrive</span><span class="sxs-lookup"><span data-stu-id="f587e-112">Connect tooOneDrive</span></span>
<span data-ttu-id="f587e-113">邏輯應用程式可以存取任何服務之前，您先建立*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="f587e-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="f587e-114">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="f587e-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="f587e-115">例如，tooconnect tooOneDrive，您必須先 OneDrive*連接*。</span><span class="sxs-lookup"><span data-stu-id="f587e-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="f587e-116">toocreate 連線，請輸入您通常會使用您想要的 tooconnect tooaccess hello 服務的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="f587e-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="f587e-117">因此，使用 OneDrive，請輸入 hello 認證 tooyour OneDrive 帳戶 toocreate hello 連接。</span><span class="sxs-lookup"><span data-stu-id="f587e-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="f587e-118">建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="f587e-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="f587e-119">使用觸發程序</span><span class="sxs-lookup"><span data-stu-id="f587e-119">Use a trigger</span></span>
<span data-ttu-id="f587e-120">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="f587e-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="f587e-121">觸發程序 「 輪詢"hello 服務以間隔和您想要的頻率。</span><span class="sxs-lookup"><span data-stu-id="f587e-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="f587e-122">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="f587e-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="f587e-123">Hello 邏輯應用程式中，輸入 「 onedrive"tooget hello 觸發程序的清單：</span><span class="sxs-lookup"><span data-stu-id="f587e-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="f587e-124">選取 [當檔案遭到修改時]。</span><span class="sxs-lookup"><span data-stu-id="f587e-124">Select **When a file is modified**.</span></span> <span data-ttu-id="f587e-125">如果連接已存在，請選取 hello 顯示選擇器 按鈕 tooselect 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f587e-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="f587e-126">如果您在提示的 toosign，然後輸入 hello 登詳細資料 toocreate hello 連接中。</span><span class="sxs-lookup"><span data-stu-id="f587e-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="f587e-127">[建立 hello 連接](connectors-create-api-onedrive.md#create-the-connection)本主題列出 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="f587e-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f587e-128">在此範例中，hello 邏輯應用程式時執行的檔案會更新您所選擇的 hello 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f587e-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="f587e-129">這個觸發程序，toosee hello 結果加入另一個傳送一封電子郵件給您的動作。</span><span class="sxs-lookup"><span data-stu-id="f587e-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="f587e-130">例如，新增 hello Office 365 Outlook*傳送電子郵件*電子郵件寄給您更新檔案時的動作。</span><span class="sxs-lookup"><span data-stu-id="f587e-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="f587e-131">選取 hello**編輯**按鈕，然後設定 hello**頻率**和**間隔**值。</span><span class="sxs-lookup"><span data-stu-id="f587e-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="f587e-132">例如，如果您想 hello 觸發程序 toopoll 每隔 15 分鐘，然後設定 hello**頻率**太**分鐘**，並設定 hello**間隔**太**15**.</span><span class="sxs-lookup"><span data-stu-id="f587e-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="f587e-133">**儲存**您的變更 （hello 工具列的左上的角）。</span><span class="sxs-lookup"><span data-stu-id="f587e-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="f587e-134">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="f587e-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="f587e-135">使用動作</span><span class="sxs-lookup"><span data-stu-id="f587e-135">Use an action</span></span>
<span data-ttu-id="f587e-136">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="f587e-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="f587e-137">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="f587e-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="f587e-138">選取加號 hello。</span><span class="sxs-lookup"><span data-stu-id="f587e-138">Select hello plus sign.</span></span> <span data-ttu-id="f587e-139">您會看到幾個選擇：**將動作加入**，**加入條件**，或其中一個 hello**詳細**選項。</span><span class="sxs-lookup"><span data-stu-id="f587e-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="f587e-140">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="f587e-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="f587e-141">在 [hello] 文字方塊中，輸入 「 onedrive"tooget 所有 hello 可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="f587e-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="f587e-142">在我們的範例中，選擇 [OneDrive - 建立檔案]。</span><span class="sxs-lookup"><span data-stu-id="f587e-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="f587e-143">如果連接已存在，然後選取 hello**資料夾路徑**tooput hello 檔案中，輸入 hello**檔案名稱**，然後選擇 hello**檔案內容**您想要：</span><span class="sxs-lookup"><span data-stu-id="f587e-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="f587e-144">如果系統提示您輸入 hello 連接資訊，然後輸入 hello 詳細資料 toocreate hello 連接。</span><span class="sxs-lookup"><span data-stu-id="f587e-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="f587e-145">[建立 hello 連接](connectors-create-api-onedrive.md#create-the-connection)本主題說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="f587e-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f587e-146">在此範例中，我們會在 OneDrive 資料夾建立新檔案。</span><span class="sxs-lookup"><span data-stu-id="f587e-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="f587e-147">您可以使用輸出從另一個觸發程序 toocreate hello OneDrive 檔案。</span><span class="sxs-lookup"><span data-stu-id="f587e-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="f587e-148">例如，新增 hello Office 365 Outlook*新的電子郵件送達時*觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f587e-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="f587e-149">然後新增 hello OneDrive*建立檔案*使用 ForEach toocreate hello 新的檔案在 OneDrive 中的 hello 附件和內容類型欄位的動作。</span><span class="sxs-lookup"><span data-stu-id="f587e-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="f587e-150">**儲存**您的變更 （hello 工具列的左上的角）。</span><span class="sxs-lookup"><span data-stu-id="f587e-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="f587e-151">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="f587e-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="f587e-152">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="f587e-152">Connector-specific details</span></span>

<span data-ttu-id="f587e-153">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/onedriveconnector/)。</span><span class="sxs-lookup"><span data-stu-id="f587e-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f587e-154">其他連接器</span><span class="sxs-lookup"><span data-stu-id="f587e-154">More connectors</span></span>
<span data-ttu-id="f587e-155">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="f587e-155">Go back toohello [APIs list](apis-list.md).</span></span>
