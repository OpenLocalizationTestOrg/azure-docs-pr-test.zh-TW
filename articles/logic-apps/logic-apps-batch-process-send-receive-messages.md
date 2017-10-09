---
title: "aaaBatch 處理訊息，做為群組或集合-Azure 邏輯應用程式 |Microsoft 文件"
description: "傳送和接收訊息以便在邏輯應用程式中批次處理"
keywords: "批次, 批次程序"
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="ecd59-104">傳送、接收，並在邏輯應用程式中批次處理訊息</span><span class="sxs-lookup"><span data-stu-id="ecd59-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="ecd59-105">tooprocess 訊息群組在一起，您可以傳送資料的項目或訊息，tooa*批次*，然後以批次中處理這些項目。</span><span class="sxs-lookup"><span data-stu-id="ecd59-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="ecd59-106">當您想要確定資料項目 toomake 中以特定方式分組和都會一起處理，則這個方法會很有用。</span><span class="sxs-lookup"><span data-stu-id="ecd59-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="ecd59-107">您可以建立以批次接收項目，使用 hello 的 logic apps**批次**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ecd59-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="ecd59-108">然後，您可以建立使用 hello 傳送項目 tooa 批次的 logic apps**批次**動作。</span><span class="sxs-lookup"><span data-stu-id="ecd59-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="ecd59-109">本主題示範如何透過執行這些工作，建置批次解決方案：</span><span class="sxs-lookup"><span data-stu-id="ecd59-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="ecd59-110">[建立邏輯應用程式，以批次接收並收集項目](#batch-receiver)。</span><span class="sxs-lookup"><span data-stu-id="ecd59-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="ecd59-111">這個 「 批次接收者 」 邏輯應用程式指定 hello 批次名稱和版本準則 toomeet 之前釋出 hello 接收者邏輯應用程式，並處理項目。</span><span class="sxs-lookup"><span data-stu-id="ecd59-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="ecd59-112">[建立邏輯應用程式所傳送的項目 tooa 批次](#batch-sender)。</span><span class="sxs-lookup"><span data-stu-id="ecd59-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="ecd59-113">這個 「 批次傳送者 」 的邏輯應用程式指定的位置 toosend 項目，必須是現有的批次接收者邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecd59-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="ecd59-114">您可以也指定唯一的索引鍵，例如客戶編號、 太 「 分割 」，或將分割成幾個子集該索引鍵為基礎的 hello 目標批次。</span><span class="sxs-lookup"><span data-stu-id="ecd59-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="ecd59-115">這樣一來，所有具有該索引鍵的項目都會一起收集並處理。</span><span class="sxs-lookup"><span data-stu-id="ecd59-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="ecd59-116">需求</span><span class="sxs-lookup"><span data-stu-id="ecd59-116">Requirements</span></span>

<span data-ttu-id="ecd59-117">toofollow 此範例中，您需要這些項目：</span><span class="sxs-lookup"><span data-stu-id="ecd59-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="ecd59-118">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ecd59-118">An Azure subscription.</span></span> <span data-ttu-id="ecd59-119">如果您沒有訂用帳戶，您可以[開始使用免費 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="ecd59-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="ecd59-120">否則，您可以[註冊隨用隨付訂用帳戶](https://azure.microsoft.com/pricing/purchase-options/)。</span><span class="sxs-lookup"><span data-stu-id="ecd59-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="ecd59-121">相關的基本知識[如何 toocreate 邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="ecd59-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="ecd59-122">電子郵件帳戶與任何 [Azure Logic Apps 所支援的電子郵件提供者](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="ecd59-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="ecd59-123">建立以批次接收訊息的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ecd59-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="ecd59-124">您可以傳送訊息 tooa 批次之前，您必須先使用 hello 建立 「 批次接收者 」 邏輯應用程式**批次**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ecd59-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="ecd59-125">這樣一來，當您建立 hello 寄件者邏輯應用程式時，可以選取這個接收器邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecd59-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="ecd59-126">Hello 收件者，您可以指定 hello 批次名稱、 釋放準則和其他設定。</span><span class="sxs-lookup"><span data-stu-id="ecd59-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="ecd59-127">寄件者的 logic apps 需要知道其中 toosend 項目，而接收器邏輯應用程式不需要 tooknow hello 寄件者有關的任何項目。</span><span class="sxs-lookup"><span data-stu-id="ecd59-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="ecd59-128">在 hello [Azure 入口網站](https://portal.azure.com)，建立邏輯應用程式具有此名稱:"BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="ecd59-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="ecd59-129">在邏輯應用程式設計師中，新增 hello**批次**觸發程序，用來啟動您的邏輯應用程式工作流程。</span><span class="sxs-lookup"><span data-stu-id="ecd59-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="ecd59-130">在 hello 搜尋方塊中輸入"batch"做為您的篩選器。</span><span class="sxs-lookup"><span data-stu-id="ecd59-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="ecd59-131">選取此觸發程序：**批次 – 批次訊息**</span><span class="sxs-lookup"><span data-stu-id="ecd59-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![新增批次觸發程序](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="ecd59-133">提供 hello 批次中的名稱，然後指定準則來釋放 hello 批次，例如：</span><span class="sxs-lookup"><span data-stu-id="ecd59-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="ecd59-134">**批次名稱**: hello 用名稱 tooidentify hello 批次，也就是在此範例中的"TestBatch"。</span><span class="sxs-lookup"><span data-stu-id="ecd59-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="ecd59-135">**訊息計數**： 釋放進行處理，也就是"5"在此範例之前，做為批次 hello 訊息 toohold 數目。</span><span class="sxs-lookup"><span data-stu-id="ecd59-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![提供批次觸發程序詳細資料](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="ecd59-137">加入另一個 hello 批次觸發程序引發時傳送電子郵件的動作。</span><span class="sxs-lookup"><span data-stu-id="ecd59-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="ecd59-138">每個時間 hello 批次有五個項目，hello 邏輯應用程式傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ecd59-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="ecd59-139">Hello 批次觸發程序，在底下選擇**+ 新增步驟** > **將動作加入**。</span><span class="sxs-lookup"><span data-stu-id="ecd59-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="ecd59-140">在 hello 搜尋方塊中輸入"email"做為您的篩選器。</span><span class="sxs-lookup"><span data-stu-id="ecd59-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="ecd59-141">根據您的電子郵件提供者，選取電子郵件連接器。</span><span class="sxs-lookup"><span data-stu-id="ecd59-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="ecd59-142">例如，如果您有工作或學校帳戶時，選取 hello Office 365 Outlook 連接器。</span><span class="sxs-lookup"><span data-stu-id="ecd59-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="ecd59-143">如果您有 Gmail 帳戶，請選取 hello Gmail 連接器。</span><span class="sxs-lookup"><span data-stu-id="ecd59-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="ecd59-144">為您的連接器選取此動作： **{*電子郵件提供者*} - 傳送電子郵件**</span><span class="sxs-lookup"><span data-stu-id="ecd59-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="ecd59-145">例如：</span><span class="sxs-lookup"><span data-stu-id="ecd59-145">For example:</span></span>

      ![為您的電子郵件提供者選取「傳送電子郵件」動作](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="ecd59-147">如果您先前未建立電子郵件提供者的連線，請提供您的電子郵件認證，以便當系統提示您時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ecd59-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="ecd59-148">深入了解[驗證您的電子郵件認證](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ecd59-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="ecd59-149">設定您剛才加入的 hello 動作 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="ecd59-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="ecd59-150">在 hello**至**方塊中，輸入 hello 收件者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ecd59-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="ecd59-151">為了測試用途，您可以使用自己的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ecd59-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="ecd59-152">在 hello**主旨**方塊中，當 hello**動態內容**清單出現時，請選取 hello**資料分割名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="ecd59-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     ![從 hello [動態內容] 清單中，選取 [資料分割名稱]](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="ecd59-154">在更新版本的區段中，您可以指定除以 hello 目標批次，邏輯到唯一的資料分割索引鍵設定 toowhere 您可以傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="ecd59-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="ecd59-155">每個集合都 hello 寄件者邏輯應用程式所產生的唯一數字。</span><span class="sxs-lookup"><span data-stu-id="ecd59-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="ecd59-156">這項功能可讓您使用多個子集的單一批次，並定義您所提供的 hello 名稱與每個子集。</span><span class="sxs-lookup"><span data-stu-id="ecd59-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="ecd59-157">在 hello**主體**方塊中，當 hello**動態內容**清單出現時，請選取 hello**訊息識別碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="ecd59-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     ![對於 [內文]，選取 [訊息識別碼]](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="ecd59-159">Hello 輸入 hello 傳送電子郵件動作是陣列，因為 hello 設計工具自動加入**每個**圈 hello**傳送電子郵件**動作。</span><span class="sxs-lookup"><span data-stu-id="ecd59-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="ecd59-160">此迴圈 hello 內部上執行動作 hello 批次中每個項目。</span><span class="sxs-lookup"><span data-stu-id="ecd59-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="ecd59-161">因此，與 hello 批次觸發程序組 toofive 項目，您會取得每個時間 hello 觸發程序引發的五個電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ecd59-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="ecd59-162">既然您建立了批次接收者邏輯應用程式，請儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecd59-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![儲存您的邏輯應用程式](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="ecd59-164">建立傳送訊息 tooa 批次的 logic apps</span><span class="sxs-lookup"><span data-stu-id="ecd59-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="ecd59-165">現在建立傳送嗨接收者邏輯應用程式所定義的項目 toohello 批次的一或多個邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecd59-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="ecd59-166">Hello 寄件者，您可以指定 hello 接收者邏輯應用程式和批次名稱、 訊息內容和任何其他設定。</span><span class="sxs-lookup"><span data-stu-id="ecd59-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="ecd59-167">您可以選擇提供唯一的資料分割索引鍵 toodivide hello 批次至子集 toocollect 項目與該索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ecd59-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="ecd59-168">寄件者的 logic apps 需要知道其中 toosend 項目，而接收器邏輯應用程式不需要 tooknow hello 寄件者有關的任何項目。</span><span class="sxs-lookup"><span data-stu-id="ecd59-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="ecd59-169">建立具有名稱 "BatchSender" 的另一個邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ecd59-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="ecd59-170">在 hello 搜尋方塊中輸入"recurrence"做為您的篩選器。</span><span class="sxs-lookup"><span data-stu-id="ecd59-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="ecd59-171">選取此觸發程序：**排程 - 重複**</span><span class="sxs-lookup"><span data-stu-id="ecd59-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![加入 hello"排程 Recurrence"觸發程序](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="ecd59-173">設定每隔一分鐘 hello 頻率和間隔 toorun hello 寄件者邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecd59-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![設定重複觸發程序的頻率和間隔](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="ecd59-175">加入新的步驟，以便傳送郵件 tooa 批次。</span><span class="sxs-lookup"><span data-stu-id="ecd59-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="ecd59-176">Hello 循環觸發程序，在底下選擇**+ 新增步驟** > **將動作加入**。</span><span class="sxs-lookup"><span data-stu-id="ecd59-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="ecd59-177">在 hello 搜尋方塊中輸入"batch"做為您的篩選器。</span><span class="sxs-lookup"><span data-stu-id="ecd59-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="ecd59-178">選取此動作：**傳送訊息 toobatch – 選擇批次觸發程序的 Logic Apps 工作流程**</span><span class="sxs-lookup"><span data-stu-id="ecd59-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![選取 [傳送郵件 toobatch]](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="ecd59-180">現在，選取您先前建立的 "BatchReceiver" 邏輯應用程式，它現在會顯示為動作。</span><span class="sxs-lookup"><span data-stu-id="ecd59-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![選取「批次接收者」邏輯應用程式](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="ecd59-182">hello 清單也會顯示有批次觸發程序的任何其他邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecd59-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="ecd59-183">設定 hello 批次屬性。</span><span class="sxs-lookup"><span data-stu-id="ecd59-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="ecd59-184">**批次名稱**: hello hello 接收者邏輯應用程式，其 「 TestBatch 「 在此範例中，並會在執行階段進行驗證所定義的批次名稱。</span><span class="sxs-lookup"><span data-stu-id="ecd59-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="ecd59-185">請確定您不要變更 hello 批次名稱必須符合 hello hello 接收者邏輯應用程式所指定的批次名稱。</span><span class="sxs-lookup"><span data-stu-id="ecd59-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="ecd59-186">變更 hello 批次名稱會導致邏輯應用程式 toofail hello 寄件者。</span><span class="sxs-lookup"><span data-stu-id="ecd59-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="ecd59-187">**訊息內容**: hello 的 toosend 訊息內容。</span><span class="sxs-lookup"><span data-stu-id="ecd59-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="ecd59-188">例如，將此運算式插入到 hello 訊息內容傳送 toohello 批次目前的日期和時間 hello:</span><span class="sxs-lookup"><span data-stu-id="ecd59-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="ecd59-189">當 hello**動態內容**清單出現時，選擇 **運算式**。</span><span class="sxs-lookup"><span data-stu-id="ecd59-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="ecd59-190">輸入 hello 運算式**utcnow()**，然後選擇 **確定**。</span><span class="sxs-lookup"><span data-stu-id="ecd59-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        ![在 [訊息內容] 中，選擇 [運算式]。](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="ecd59-193">現在設定 hello 批次的資料分割。</span><span class="sxs-lookup"><span data-stu-id="ecd59-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="ecd59-194">在 hello"BatchReceiver 」 動作，選擇  **Show advanced 選項**。</span><span class="sxs-lookup"><span data-stu-id="ecd59-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="ecd59-195">**分割區名稱**: 選用唯一的資料分割索引鍵 toouse 分配 hello 目標批次。</span><span class="sxs-lookup"><span data-stu-id="ecd59-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="ecd59-196">針對此範例，請新增運算式，產生介於 1 到 5 的隨機數字。</span><span class="sxs-lookup"><span data-stu-id="ecd59-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="ecd59-197">當 hello**動態內容**清單出現時，選擇 **運算式**。</span><span class="sxs-lookup"><span data-stu-id="ecd59-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="ecd59-198">輸入此運算式：**rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="ecd59-198">Enter this expression: **rand(1,6)**</span></span>

        ![設定目標批次的資料分割](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="ecd59-200">這個 **rand** 函式會產生一到五之間的數字。</span><span class="sxs-lookup"><span data-stu-id="ecd59-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="ecd59-201">因此您會將此批次分割成五個有編號的資料分割，此運算式會以動態方式設定。</span><span class="sxs-lookup"><span data-stu-id="ecd59-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="ecd59-202">**訊息識別碼**：選擇性的訊息識別碼，空白時是一個產生的 GUID。</span><span class="sxs-lookup"><span data-stu-id="ecd59-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="ecd59-203">針對此範例，請將這個方塊保留空白。</span><span class="sxs-lookup"><span data-stu-id="ecd59-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="ecd59-204">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecd59-204">Save your logic app.</span></span> <span data-ttu-id="ecd59-205">寄件者的邏輯應用程式現在看起來類似 toothis 範例：</span><span class="sxs-lookup"><span data-stu-id="ecd59-205">Your sender logic app now looks similar toothis example:</span></span>

   ![儲存您的傳送者邏輯應用程式](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="ecd59-207">儲存邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ecd59-207">Test your logic apps</span></span>

<span data-ttu-id="ecd59-208">tootest 您批次處理方案，將保留在幾分鐘後執行邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecd59-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="ecd59-209">過期，啟動 取得五個群組中的電子郵件時，所有的 hello 相同資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ecd59-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="ecd59-210">BatchSender 邏輯應用程式會每分鐘執行、 產生隨機數字，介於 1 到 5，並使用這個產生的數字為 hello hello 目標批次的資料分割索引鍵會傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="ecd59-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="ecd59-211">每次 hello 批次有五個項目以 hello 相同的資料分割索引鍵，BatchReceiver 邏輯應用程式就會引發並傳送郵件的每個訊息。</span><span class="sxs-lookup"><span data-stu-id="ecd59-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecd59-212">當您完成測試，請確定您停用 hello BatchSender 邏輯應用程式 toostop 傳送訊息，並避免超載收件匣。</span><span class="sxs-lookup"><span data-stu-id="ecd59-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecd59-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecd59-213">Next steps</span></span>

* [<span data-ttu-id="ecd59-214">使用 JSON 建置於邏輯應用程式定義上</span><span class="sxs-lookup"><span data-stu-id="ecd59-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="ecd59-215">在 Visual Studio 中使用 Azure Logic Apps 和 Functions 建置邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ecd59-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="ecd59-216">適用於邏輯應用程式的例外狀況處理與記錄錯誤</span><span class="sxs-lookup"><span data-stu-id="ecd59-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
