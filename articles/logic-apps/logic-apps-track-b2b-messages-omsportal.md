---
title: "Operations Management Suite Azure 邏輯應用程式中的 aaaTrack B2B 訊息 |Microsoft 文件"
description: "使用 Azure Log Analytics 追蹤 Operations Management Suite (OMS) 中整合帳戶和邏輯應用程式的 B2B 通訊"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="689ae-103">在 hello Microsoft Operations Management Suite (OMS) 中的追蹤 B2B 通訊</span><span class="sxs-lookup"><span data-stu-id="689ae-103">Track B2B communication in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="689ae-104">在您透過整合帳戶設定兩個執行中商務程序或應用程式之間的 B2B 通訊之後，這些實體也可以彼此交換訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="689ae-105">toocheck 是否正確處理這些訊息，您可以追蹤 X12，AS2 和 EDIFACT 訊息與[Azure Log Analytics](../log-analytics/log-analytics-overview.md)在 hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="689ae-105">toocheck whether these messages are processed correctly, you can track AS2, X12, and EDIFACT messages with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="689ae-106">例如，您可以使用這些網頁追蹤功能來追蹤訊息：</span><span class="sxs-lookup"><span data-stu-id="689ae-106">For example, you can use these web-based tracking capabilities for tracking messages:</span></span>

* <span data-ttu-id="689ae-107">訊息計數和狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-107">Message count and status</span></span>
* <span data-ttu-id="689ae-108">通知狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-108">Acknowledgments status</span></span>
* <span data-ttu-id="689ae-109">訊息與通知的相互關聯</span><span class="sxs-lookup"><span data-stu-id="689ae-109">Correlate messages with acknowledgments</span></span>
* <span data-ttu-id="689ae-110">失敗的詳細錯誤描述</span><span class="sxs-lookup"><span data-stu-id="689ae-110">Detailed error descriptions for failures</span></span>
* <span data-ttu-id="689ae-111">搜尋功能</span><span class="sxs-lookup"><span data-stu-id="689ae-111">Search capabilities</span></span>

## <a name="requirements"></a><span data-ttu-id="689ae-112">需求</span><span class="sxs-lookup"><span data-stu-id="689ae-112">Requirements</span></span>

* <span data-ttu-id="689ae-113">已設定診斷記錄的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="689ae-113">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="689ae-114">深入了解[如何 toocreate 邏輯應用程式](logic-apps-create-a-logic-app.md)和[如何該邏輯應用程式的記錄 tooset](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="689ae-114">Learn [how toocreate a logic app](logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="689ae-115">已設定監視和記錄的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="689ae-115">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="689ae-116">深入了解[如何 toocreate 整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)和[如何監視和記錄該帳戶的總 tooset](../logic-apps/logic-apps-monitor-b2b-message.md)。</span><span class="sxs-lookup"><span data-stu-id="689ae-116">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="689ae-117">如果您還沒有這麼做，[發行分析的診斷資料 tooLog](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)在 OMS 中。</span><span class="sxs-lookup"><span data-stu-id="689ae-117">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) in OMS.</span></span>

> [!NOTE]
> <span data-ttu-id="689ae-118">您雖然符合 hello 先前的需求之後，您應該有 hello 中的工作區[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="689ae-118">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="689ae-119">您應該使用 hello 追蹤您在 OMS 中的 B2B 通訊的同一個 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="689ae-119">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="689ae-120">如果您沒有 OMS 工作區，了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="689ae-120">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a><span data-ttu-id="689ae-121">新增 hello 邏輯應用程式 B2B 解決方案 toohello Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="689ae-121">Add hello Logic Apps B2B solution toohello Operations Management Suite (OMS)</span></span>

<span data-ttu-id="689ae-122">toohave OMS 追蹤 B2B 訊息的應用程式邏輯，您必須新增 hello**邏輯應用程式 B2B**方案 toohello OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="689ae-122">toohave OMS track B2B messages for your logic app, you must add hello **Logic Apps B2B** solution toohello OMS portal.</span></span> <span data-ttu-id="689ae-123">深入了解[加入解決方案 tooOMS](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="689ae-123">Learn more about [adding solutions tooOMS](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="689ae-124">在 hello [Azure 入口網站](https://portal.azure.com)，選擇**更服務**。</span><span class="sxs-lookup"><span data-stu-id="689ae-124">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="689ae-125">搜尋 "log analytics"，然後選擇 [Log Analytics]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="689ae-125">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![尋找 Log Analytics](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. <span data-ttu-id="689ae-127">在 [Log Analytics] 下，尋找並選取 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="689ae-127">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![選取 OMS 工作區](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. <span data-ttu-id="689ae-129">在 [管理] 下，選擇 [OMS 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="689ae-129">Under **Management**, choose **OMS Portal**.</span></span>

   ![選擇 OMS 入口網站](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. <span data-ttu-id="689ae-131">Hello OMS 首頁上開啟之後，請選擇**解決方案資源庫**。</span><span class="sxs-lookup"><span data-stu-id="689ae-131">After hello OMS home page opens, choose **Solutions Gallery**.</span></span>    

   ![選取方案庫](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. <span data-ttu-id="689ae-133">在 [所有解決方案] 下，尋找並選擇 [Logic Apps B2B]。</span><span class="sxs-lookup"><span data-stu-id="689ae-133">Under **All solutions**, find and choose **Logic Apps B2B**.</span></span>     

   ![選擇 Logic Apps B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. <span data-ttu-id="689ae-135">在 [Logic Apps B2B] 下，選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="689ae-135">Under **Logic Apps B2B**, choose **Add**.</span></span>

   ![選擇 [新增]](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   <span data-ttu-id="689ae-137">在 hello OMS 首頁上，hello 磚**邏輯應用程式 B2B 訊息**隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="689ae-137">On hello OMS home page, hello tile for **Logic Apps B2B Messages** now appears.</span></span> 
   <span data-ttu-id="689ae-138">當處理 B2B 訊息時，此磚會更新 hello 訊息計數。</span><span class="sxs-lookup"><span data-stu-id="689ae-138">This tile updates hello message count when your B2B messages are processed.</span></span>

   ![OMS 首頁、[Logic Apps B2B 訊息] 磚](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a><span data-ttu-id="689ae-140">追蹤訊息狀態和 hello Operations Management Suite 中的詳細資料</span><span class="sxs-lookup"><span data-stu-id="689ae-140">Track message status and details in hello Operations Management Suite</span></span>

1. <span data-ttu-id="689ae-141">處理 B2B 訊息之後，您可以檢視 hello 狀態和適用於這些訊息的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="689ae-141">After your B2B messages are processed, you can view hello status and details for those messages.</span></span> <span data-ttu-id="689ae-142">在 hello OMS 首頁上，選擇 hello**邏輯應用程式 B2B 訊息**磚。</span><span class="sxs-lookup"><span data-stu-id="689ae-142">On hello OMS home page, choose hello **Logic Apps B2B Messages** tile.</span></span>

   ![更新的訊息計數](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > <span data-ttu-id="689ae-144">根據預設，hello**邏輯應用程式 B2B 訊息**磚會顯示一天為基礎的資料。</span><span class="sxs-lookup"><span data-stu-id="689ae-144">By default, hello **Logic Apps B2B Messages** tile shows data based on a single day.</span></span> <span data-ttu-id="689ae-145">toochange hello 資料範圍 tooa 不同的間隔中，選擇 hello 頁面頂端的 hello OMS hello 範圍控制項：</span><span class="sxs-lookup"><span data-stu-id="689ae-145">toochange hello data scope tooa different interval, choose hello scope control at hello top of hello OMS page:</span></span>
   > 
   > ![變更資料範圍](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. <span data-ttu-id="689ae-147">在 hello 訊息狀態儀表板出現之後，您可以檢視特定訊息類型，顯示資料是根據一天的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="689ae-147">After hello message status dashboard appears, you can view more details for a specific message type, which shows data based on a single day.</span></span> <span data-ttu-id="689ae-148">選擇 hello 磚**AS2**， **X12**，或**EDIFACT**。</span><span class="sxs-lookup"><span data-stu-id="689ae-148">Choose hello tile for **AS2**, **X12**, or **EDIFACT**.</span></span>

   ![檢視訊息狀態](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   <span data-ttu-id="689ae-150">會針對您所選擇的磚顯示訊息清單。</span><span class="sxs-lookup"><span data-stu-id="689ae-150">A list of messages appears for your chosen tile.</span></span> 
   <span data-ttu-id="689ae-151">toolearn 進一步了解 hello 屬性對於每個訊息類型，請參閱這些訊息屬性的描述：</span><span class="sxs-lookup"><span data-stu-id="689ae-151">toolearn more about hello properties for each message type, see these message property descriptions:</span></span>

   * [<span data-ttu-id="689ae-152">AS2 訊息屬性</span><span class="sxs-lookup"><span data-stu-id="689ae-152">AS2 message properties</span></span>](#as2-message-properties)
   * [<span data-ttu-id="689ae-153">X12 訊息屬性</span><span class="sxs-lookup"><span data-stu-id="689ae-153">X12 message properties</span></span>](#x12-message-properties)
   * [<span data-ttu-id="689ae-154">EDIFACT 訊息屬性</span><span class="sxs-lookup"><span data-stu-id="689ae-154">EDIFACT message properties</span></span>](#EDIFACT-message-properties)

   <span data-ttu-id="689ae-155">例如，AS2 訊息清單可能如下：</span><span class="sxs-lookup"><span data-stu-id="689ae-155">For example, here's what an AS2 message list might look like:</span></span>

   ![檢視 AS2 訊息](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. <span data-ttu-id="689ae-157">特定訊息，tooview 或匯出的 hello 輸入和輸出選取這些訊息，然後選擇**下載**。</span><span class="sxs-lookup"><span data-stu-id="689ae-157">tooview or export hello inputs and outputs for specific messages, select those messages, and choose **Download**.</span></span> <span data-ttu-id="689ae-158">則會提示您，儲存 hello.zip 檔案 tooyour 本機電腦，並解壓縮該檔案。</span><span class="sxs-lookup"><span data-stu-id="689ae-158">When you're prompted, save hello .zip file tooyour local computer, and then extract that file.</span></span> 

   <span data-ttu-id="689ae-159">hello 解壓縮的資料夾會包含每個選取之訊息的資料夾。</span><span class="sxs-lookup"><span data-stu-id="689ae-159">hello extracted folder includes a folder for each selected message.</span></span> 
   <span data-ttu-id="689ae-160">如果您設定通知，hello 訊息資料夾也會包含認可詳細資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="689ae-160">If you set up acknowledgements, hello message folder also includes files with acknowledgement details.</span></span> 
   <span data-ttu-id="689ae-161">每個訊息資料夾都會至少有這些檔案：</span><span class="sxs-lookup"><span data-stu-id="689ae-161">Each message folder has at least these files:</span></span> 
   
   * <span data-ttu-id="689ae-162">人類看得懂的檔案，以 hello 輸入及輸出內容承載詳細資料</span><span class="sxs-lookup"><span data-stu-id="689ae-162">Human-readable files with hello input payload and output payload details</span></span>
   * <span data-ttu-id="689ae-163">編碼的檔案具有 hello 輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="689ae-163">Encoded files with hello inputs and outputs</span></span>

   <span data-ttu-id="689ae-164">對於每個訊息類型，您可以找到 hello 資料夾和檔案名稱格式：</span><span class="sxs-lookup"><span data-stu-id="689ae-164">For each message type, you can find hello folder and file name formats here:</span></span>

   * [<span data-ttu-id="689ae-165">AS2 資料夾和檔案名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-165">AS2 folder and file name formats</span></span>](#as2-folder-file-names)
   * [<span data-ttu-id="689ae-166">X12 資料夾和檔案名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-166">X12 folder and file name formats</span></span>](#x12-folder-file-names)
   * [<span data-ttu-id="689ae-167">EDIFACT 資料夾和檔案名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-167">EDIFACT folder and file name formats</span></span>](#edifact-folder-file-names)

   ![下載訊息檔案](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. <span data-ttu-id="689ae-169">tooview hello 相同的所有動作識別碼，在上執行 hello**記錄搜尋**頁面上，從 hello 訊息清單中選擇一則訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-169">tooview all actions that have hello same run ID, on hello **Log Search** page, choose a message from hello message list.</span></span>

   <span data-ttu-id="689ae-170">您可以依資料行排序這些動作，或搜尋特定結果。</span><span class="sxs-lookup"><span data-stu-id="689ae-170">You can sort these actions by column, or search for specific results.</span></span>

   ![動作以 hello 相同回合 ID](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * <span data-ttu-id="689ae-172">toosearch 預先建立的查詢結果選擇**我的最愛**。</span><span class="sxs-lookup"><span data-stu-id="689ae-172">toosearch results with prebuilt queries, choose **Favorites**.</span></span>

   * <span data-ttu-id="689ae-173">深入了解[toobuild 藉由加入篩選查詢的方式](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)。</span><span class="sxs-lookup"><span data-stu-id="689ae-173">Learn [how toobuild queries by adding filters](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md).</span></span> 
   <span data-ttu-id="689ae-174">深入了解或者[toofind 資料與記錄檔中記錄分析搜尋的方式](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="689ae-174">Or learn more about [how toofind data with log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   * <span data-ttu-id="689ae-175">toochange hello 搜尋方塊中，更新 hello 與 hello 資料行和值，您想查詢 toouse 做為篩選的查詢。</span><span class="sxs-lookup"><span data-stu-id="689ae-175">toochange query in hello search box, update hello query with hello columns and values that you want toouse as filters.</span></span>

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a><span data-ttu-id="689ae-176">AS2、X12 和 EDIFACT 訊息的屬性描述和名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-176">Property descriptions and name formats for AS2, X12, and EDIFACT messages</span></span>

<span data-ttu-id="689ae-177">對於每個訊息類型，以下是 hello 屬性說明與下載的訊息檔案的名稱格式。</span><span class="sxs-lookup"><span data-stu-id="689ae-177">For each message type, here are hello property descriptions and name formats for downloaded message files.</span></span>

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a><span data-ttu-id="689ae-178">AS2 訊息屬性描述</span><span class="sxs-lookup"><span data-stu-id="689ae-178">AS2 message property descriptions</span></span>

<span data-ttu-id="689ae-179">以下是每個 AS2 訊息的 hello 屬性描述。</span><span class="sxs-lookup"><span data-stu-id="689ae-179">Here are hello property descriptions for each AS2 message.</span></span>

| <span data-ttu-id="689ae-180">屬性</span><span class="sxs-lookup"><span data-stu-id="689ae-180">Property</span></span> | <span data-ttu-id="689ae-181">說明</span><span class="sxs-lookup"><span data-stu-id="689ae-181">Description</span></span> |
| --- | --- |
| <span data-ttu-id="689ae-182">傳送者</span><span class="sxs-lookup"><span data-stu-id="689ae-182">Sender</span></span> | <span data-ttu-id="689ae-183">中所指定的 hello 來賓夥伴**接收設定**，或在其中指定 hello 主控合作夥伴**傳送設定**AS2 協議</span><span class="sxs-lookup"><span data-stu-id="689ae-183">hello guest partner specified in **Receive Settings**, or hello host partner specified in **Send Settings** for an AS2 agreement</span></span> |
| <span data-ttu-id="689ae-184">接收者</span><span class="sxs-lookup"><span data-stu-id="689ae-184">Receiver</span></span> | <span data-ttu-id="689ae-185">中所指定的 hello 主機夥伴**接收設定**，或在其中指定 hello 來賓夥伴**傳送設定**AS2 協議</span><span class="sxs-lookup"><span data-stu-id="689ae-185">hello host partner specified in **Receive Settings**, or hello guest partner specified in **Send Settings** for an AS2 agreement</span></span> |
| <span data-ttu-id="689ae-186">邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="689ae-186">Logic App</span></span> | <span data-ttu-id="689ae-187">hello AS2 動作會設定其中的 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="689ae-187">hello logic app where hello AS2 actions are set up</span></span> |
| <span data-ttu-id="689ae-188">狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-188">Status</span></span> | <span data-ttu-id="689ae-189">hello AS2 訊息狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-189">hello AS2 message status</span></span> <br><span data-ttu-id="689ae-190">成功 = 已接收或傳送有效的 AS2 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-190">Success = Received or sent a valid AS2 message.</span></span> <span data-ttu-id="689ae-191">未設定 MDN。</span><span class="sxs-lookup"><span data-stu-id="689ae-191">No MDN is set up.</span></span> <br><span data-ttu-id="689ae-192">成功 = 已接收或傳送有效的 AS2 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-192">Success = Received or sent a valid AS2 message.</span></span> <span data-ttu-id="689ae-193">已設定並接收 MDN，或傳送 MDN。</span><span class="sxs-lookup"><span data-stu-id="689ae-193">MDN is set up and received, or MDN is sent.</span></span> <br><span data-ttu-id="689ae-194">失敗 = 已接收無效的 AS2 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-194">Failed = Received an invalid AS2 message.</span></span> <span data-ttu-id="689ae-195">未設定 MDN。</span><span class="sxs-lookup"><span data-stu-id="689ae-195">No MDN is set up.</span></span> <br><span data-ttu-id="689ae-196">暫止 = 已接收或傳送有效的 AS2 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-196">Pending = Received or sent a valid AS2 message.</span></span> <span data-ttu-id="689ae-197">已設定 MDN，並預期要有 MDN。</span><span class="sxs-lookup"><span data-stu-id="689ae-197">MDN is set up, and MDN is expected.</span></span> |
| <span data-ttu-id="689ae-198">Ack</span><span class="sxs-lookup"><span data-stu-id="689ae-198">Ack</span></span> | <span data-ttu-id="689ae-199">hello 訊息的 MDN 狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-199">hello MDN message status</span></span> <br><span data-ttu-id="689ae-200">接受 = 已接收或傳送正值的 MDN。</span><span class="sxs-lookup"><span data-stu-id="689ae-200">Accepted = Received or sent a positive MDN.</span></span> <br><span data-ttu-id="689ae-201">Pending = 等待 tooreceive 或傳送 MDN。</span><span class="sxs-lookup"><span data-stu-id="689ae-201">Pending = Waiting tooreceive or send an MDN.</span></span> <br><span data-ttu-id="689ae-202">拒絕 = 已接收或傳送負值的 MDN。</span><span class="sxs-lookup"><span data-stu-id="689ae-202">Rejected = Received or sent a negative MDN.</span></span> <br><span data-ttu-id="689ae-203">不需要 = MDN 不會設定在 hello 協議。</span><span class="sxs-lookup"><span data-stu-id="689ae-203">Not Required = MDN is not set up in hello agreement.</span></span> |
| <span data-ttu-id="689ae-204">方向</span><span class="sxs-lookup"><span data-stu-id="689ae-204">Direction</span></span> | <span data-ttu-id="689ae-205">hello AS2 訊息的方向</span><span class="sxs-lookup"><span data-stu-id="689ae-205">hello AS2 message direction</span></span> |
| <span data-ttu-id="689ae-206">相互關連識別碼</span><span class="sxs-lookup"><span data-stu-id="689ae-206">Correlation ID</span></span> | <span data-ttu-id="689ae-207">相互關聯的所有 hello 觸發程序和動作邏輯應用程式中的 hello 識別碼</span><span class="sxs-lookup"><span data-stu-id="689ae-207">hello ID that correlates all hello triggers and actions in a logic app</span></span> |
| <span data-ttu-id="689ae-208">訊息識別碼</span><span class="sxs-lookup"><span data-stu-id="689ae-208">Message ID</span></span> | <span data-ttu-id="689ae-209">hello AS2 訊息識別碼，從 hello AS2 訊息標頭</span><span class="sxs-lookup"><span data-stu-id="689ae-209">hello AS2 message ID from hello AS2 message headers</span></span> |
| <span data-ttu-id="689ae-210">Timestamp</span><span class="sxs-lookup"><span data-stu-id="689ae-210">Timestamp</span></span> | <span data-ttu-id="689ae-211">hello hello AS2 動作處理 hello 訊息時的時間</span><span class="sxs-lookup"><span data-stu-id="689ae-211">hello time when hello AS2 action processed hello message</span></span> |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a><span data-ttu-id="689ae-212">所下載訊息檔案的 AS2 名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-212">AS2 name formats for downloaded message files</span></span>

<span data-ttu-id="689ae-213">以下是針對每個下載的 AS2 訊息的資料夾和檔案的 hello 名稱格式。</span><span class="sxs-lookup"><span data-stu-id="689ae-213">Here are hello name formats for each downloaded AS2 message folder and files.</span></span>

| <span data-ttu-id="689ae-214">資料夾或檔案</span><span class="sxs-lookup"><span data-stu-id="689ae-214">Folder or file</span></span> | <span data-ttu-id="689ae-215">名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-215">Name format</span></span> |
| :------------- | :---------- |
| <span data-ttu-id="689ae-216">訊息資料夾</span><span class="sxs-lookup"><span data-stu-id="689ae-216">Message folder</span></span> | <span data-ttu-id="689ae-217">[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_[訊息識別碼]\_[時間戳記]</span><span class="sxs-lookup"><span data-stu-id="689ae-217">[sender]\_[receiver]\_AS2\_[correlation-ID]\_[message-ID]\_[timestamp]</span></span> |
| <span data-ttu-id="689ae-218">輸入、輸出和通知檔案 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="689ae-218">Input, output, and if set up, acknowledgement files</span></span> | <span data-ttu-id="689ae-219">**輸入承載**：[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_input_payload.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-219">**Input payload**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_input_payload.txt</span></span> </p><span data-ttu-id="689ae-220">**輸出承載**：[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_output\_payload.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-220">**Output payload**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_output\_payload.txt</span></span> </p></p><span data-ttu-id="689ae-221">**輸入**：[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_inputs.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-221">**Inputs**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_inputs.txt</span></span> </p></p><span data-ttu-id="689ae-222">**輸出**：[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_outputs.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-222">**Outputs**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_outputs.txt</span></span> |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a><span data-ttu-id="689ae-223">X12 訊息屬性描述</span><span class="sxs-lookup"><span data-stu-id="689ae-223">X12 message property descriptions</span></span>

<span data-ttu-id="689ae-224">以下是每個 X12 的 hello 屬性描述訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-224">Here are hello property descriptions for each X12 message.</span></span>

| <span data-ttu-id="689ae-225">屬性</span><span class="sxs-lookup"><span data-stu-id="689ae-225">Property</span></span> | <span data-ttu-id="689ae-226">說明</span><span class="sxs-lookup"><span data-stu-id="689ae-226">Description</span></span> |
| --- | --- |
| <span data-ttu-id="689ae-227">傳送者</span><span class="sxs-lookup"><span data-stu-id="689ae-227">Sender</span></span> | <span data-ttu-id="689ae-228">中所指定的 hello 來賓夥伴**接收設定**，或在其中指定 hello 主控合作夥伴**傳送設定**x12 協議</span><span class="sxs-lookup"><span data-stu-id="689ae-228">hello guest partner specified in **Receive Settings**, or hello host partner specified in **Send Settings** for an X12 agreement</span></span> |
| <span data-ttu-id="689ae-229">接收者</span><span class="sxs-lookup"><span data-stu-id="689ae-229">Receiver</span></span> | <span data-ttu-id="689ae-230">中指定的 hello 主控合作夥伴**接收設定**，或在指定的 hello 來賓夥伴**傳送設定**x12 協議</span><span class="sxs-lookup"><span data-stu-id="689ae-230">hello host partner specified in **Receive Settings**, or hello guest partner specified in **Send Settings** for an X12 agreement</span></span> |
| <span data-ttu-id="689ae-231">邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="689ae-231">Logic App</span></span> | <span data-ttu-id="689ae-232">hello X12 動作會設定其中的 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="689ae-232">hello logic app where hello X12 actions are set up</span></span> |
| <span data-ttu-id="689ae-233">狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-233">Status</span></span> | <span data-ttu-id="689ae-234">hello X12 訊息狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-234">hello X12 message status</span></span> <br><span data-ttu-id="689ae-235">成功 = 已接收或傳送有效的 X12 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-235">Success = Received or sent a valid X12 message.</span></span> <span data-ttu-id="689ae-236">未設定任何功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-236">No functional ack is set up.</span></span> <br><span data-ttu-id="689ae-237">成功 = 已接收或傳送有效的 X12 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-237">Success = Received or sent a valid X12 message.</span></span> <span data-ttu-id="689ae-238">已設定和接收功能通知，或傳送功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-238">Functional ack is set up and received, or a functional ack is sent.</span></span> <br><span data-ttu-id="689ae-239">失敗 = 已接收或傳送有效的 X12 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-239">Failed = Received or sent an invalid X12 message.</span></span> <br><span data-ttu-id="689ae-240">暫止 = 已接收或傳送有效的 X12 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-240">Pending = Received or sent a valid X12 message.</span></span> <span data-ttu-id="689ae-241">已設定功能通知，並預期要有功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-241">Functional ack is set up, and a functional ack is expected.</span></span> |
| <span data-ttu-id="689ae-242">Ack</span><span class="sxs-lookup"><span data-stu-id="689ae-242">Ack</span></span> | <span data-ttu-id="689ae-243">功能認可 (997) 狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-243">Functional Ack (997) status</span></span> <br><span data-ttu-id="689ae-244">接受 = 已接收或傳送正值的功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-244">Accepted = Received or sent a positive functional ack.</span></span> <br><span data-ttu-id="689ae-245">拒絕 = 已接收或傳送負值的功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-245">Rejected = Received or sent a negative functional ack.</span></span> <br><span data-ttu-id="689ae-246">暫止 = 預期要有功能通知但未收到。</span><span class="sxs-lookup"><span data-stu-id="689ae-246">Pending = Expecting a functional ack but not received.</span></span> <br><span data-ttu-id="689ae-247">暫止的 = 產生功能通知，但無法傳送 toopartner。</span><span class="sxs-lookup"><span data-stu-id="689ae-247">Pending = Generated a functional ack but can't send toopartner.</span></span> <br><span data-ttu-id="689ae-248">不需要 = 未設定功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-248">Not Required = Functional ack is not set up.</span></span> |
| <span data-ttu-id="689ae-249">方向</span><span class="sxs-lookup"><span data-stu-id="689ae-249">Direction</span></span> | <span data-ttu-id="689ae-250">hello X12 訊息方向</span><span class="sxs-lookup"><span data-stu-id="689ae-250">hello X12 message direction</span></span> |
| <span data-ttu-id="689ae-251">相互關連識別碼</span><span class="sxs-lookup"><span data-stu-id="689ae-251">Correlation ID</span></span> | <span data-ttu-id="689ae-252">相互關聯的所有 hello 觸發程序和動作邏輯應用程式中的 hello 識別碼</span><span class="sxs-lookup"><span data-stu-id="689ae-252">hello ID that correlates all hello triggers and actions in a logic app</span></span> |
| <span data-ttu-id="689ae-253">訊息類型</span><span class="sxs-lookup"><span data-stu-id="689ae-253">Msg type</span></span> | <span data-ttu-id="689ae-254">hello EDI X 12 訊息類型</span><span class="sxs-lookup"><span data-stu-id="689ae-254">hello EDI X12 message type</span></span> |
| <span data-ttu-id="689ae-255">ICN</span><span class="sxs-lookup"><span data-stu-id="689ae-255">ICN</span></span> | <span data-ttu-id="689ae-256">hello X12 訊息的 hello 交換控制編號</span><span class="sxs-lookup"><span data-stu-id="689ae-256">hello Interchange Control Number for hello X12 message</span></span> |
| <span data-ttu-id="689ae-257">TSCN</span><span class="sxs-lookup"><span data-stu-id="689ae-257">TSCN</span></span> | <span data-ttu-id="689ae-258">hello X12 訊息的交易集控制編號 hello</span><span class="sxs-lookup"><span data-stu-id="689ae-258">hello Transaction Set Control Number for hello X12 message</span></span> |
| <span data-ttu-id="689ae-259">Timestamp</span><span class="sxs-lookup"><span data-stu-id="689ae-259">Timestamp</span></span> | <span data-ttu-id="689ae-260">hello hello X12 動作處理 hello 訊息時的時間</span><span class="sxs-lookup"><span data-stu-id="689ae-260">hello time when hello X12 action processed hello message</span></span> |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a><span data-ttu-id="689ae-261">所下載訊息檔案的 X12 名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-261">X12 name formats for downloaded message files</span></span>

<span data-ttu-id="689ae-262">以下是 hello 名稱格式，針對每個下載 X12 訊息的資料夾和檔案。</span><span class="sxs-lookup"><span data-stu-id="689ae-262">Here are hello name formats for each downloaded X12 message folder and files.</span></span>

| <span data-ttu-id="689ae-263">資料夾或檔案</span><span class="sxs-lookup"><span data-stu-id="689ae-263">Folder or file</span></span> | <span data-ttu-id="689ae-264">名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-264">Name format</span></span> |
| :------------- | :---------- |
| <span data-ttu-id="689ae-265">訊息資料夾</span><span class="sxs-lookup"><span data-stu-id="689ae-265">Message folder</span></span> | <span data-ttu-id="689ae-266">[寄件者]\_[接收者]\_X12\_[交換控制編號]\_[通用控制編號]\_[交易集控制編號]\_[時間戳記]</span><span class="sxs-lookup"><span data-stu-id="689ae-266">[sender]\_[receiver]\_X12\_[interchange-control-number]\_[global-control-number]\_[transaction-set-control-number]\_[timestamp]</span></span> |
| <span data-ttu-id="689ae-267">輸入、輸出和通知檔案 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="689ae-267">Input, output, and if set up, acknowledgement files</span></span> | <span data-ttu-id="689ae-268">**輸入承載**：[寄件者]\_[接收者]\_X12\_[交換控制編號]\_input_payload.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-268">**Input payload**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_input_payload.txt</span></span> </p><span data-ttu-id="689ae-269">**輸出承載**：[寄件者]\_[接收者]\_X12\_[交換控制編號]\_output\_payload.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-269">**Output payload**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_output\_payload.txt</span></span> </p></p><span data-ttu-id="689ae-270">**輸入**：[寄件者]\_[接收者]\_X12\_[交換控制編號]\_inputs.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-270">**Inputs**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_inputs.txt</span></span> </p></p><span data-ttu-id="689ae-271">**輸出**：[寄件者]\_[接收者]\_X12\_[交換控制編號]\_outputs.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-271">**Outputs**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_outputs.txt</span></span> |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a><span data-ttu-id="689ae-272">EDIFACT 訊息屬性描述</span><span class="sxs-lookup"><span data-stu-id="689ae-272">EDIFACT message property descriptions</span></span>

<span data-ttu-id="689ae-273">以下是每個 EDIFACT 訊息的 hello 屬性描述。</span><span class="sxs-lookup"><span data-stu-id="689ae-273">Here are hello property descriptions for each EDIFACT message.</span></span>

| <span data-ttu-id="689ae-274">屬性</span><span class="sxs-lookup"><span data-stu-id="689ae-274">Property</span></span> | <span data-ttu-id="689ae-275">說明</span><span class="sxs-lookup"><span data-stu-id="689ae-275">Description</span></span> |
| --- | --- |
| <span data-ttu-id="689ae-276">傳送者</span><span class="sxs-lookup"><span data-stu-id="689ae-276">Sender</span></span> | <span data-ttu-id="689ae-277">中所指定的 hello 來賓夥伴**接收設定**，或在其中指定 hello 主控合作夥伴**傳送設定**EDIFACT 協議</span><span class="sxs-lookup"><span data-stu-id="689ae-277">hello guest partner specified in **Receive Settings**, or hello host partner specified in **Send Settings** for an EDIFACT agreement</span></span> |
| <span data-ttu-id="689ae-278">接收者</span><span class="sxs-lookup"><span data-stu-id="689ae-278">Receiver</span></span> | <span data-ttu-id="689ae-279">中所指定的 hello 主機夥伴**接收設定**，或在其中指定 hello 來賓夥伴**傳送設定**EDIFACT 協議</span><span class="sxs-lookup"><span data-stu-id="689ae-279">hello host partner specified in **Receive Settings**, or hello guest partner specified in **Send Settings** for an EDIFACT agreement</span></span> |
| <span data-ttu-id="689ae-280">邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="689ae-280">Logic App</span></span> | <span data-ttu-id="689ae-281">hello EDIFACT 動作會設定其中的 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="689ae-281">hello logic app where hello EDIFACT actions are set up</span></span> |
| <span data-ttu-id="689ae-282">狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-282">Status</span></span> | <span data-ttu-id="689ae-283">hello EDIFACT 訊息狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-283">hello EDIFACT message status</span></span> <br><span data-ttu-id="689ae-284">成功 = 已接收或傳送有效的 EDIFACT 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-284">Success = Received or sent a valid EDIFACT message.</span></span> <span data-ttu-id="689ae-285">未設定任何功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-285">No functional ack is set up.</span></span> <br><span data-ttu-id="689ae-286">成功 = 已接收或傳送有效的 EDIFACT 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-286">Success = Received or sent a valid EDIFACT message.</span></span> <span data-ttu-id="689ae-287">已設定和接收功能通知，或傳送功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-287">Functional ack is set up and received, or a functional ack is sent.</span></span> <br><span data-ttu-id="689ae-288">失敗 = 已接收或傳送有效的 EDIFACT 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-288">Failed = Received or sent an invalid EDIFACT message</span></span> <br><span data-ttu-id="689ae-289">暫止 = 已接收或傳送有效的 EDIFACT 訊息。</span><span class="sxs-lookup"><span data-stu-id="689ae-289">Pending = Received or sent a valid EDIFACT message.</span></span> <span data-ttu-id="689ae-290">已設定功能通知，並預期要有功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-290">Functional ack is set up, and a functional ack is expected.</span></span> |
| <span data-ttu-id="689ae-291">Ack</span><span class="sxs-lookup"><span data-stu-id="689ae-291">Ack</span></span> | <span data-ttu-id="689ae-292">功能認可 (997) 狀態</span><span class="sxs-lookup"><span data-stu-id="689ae-292">Functional Ack (997) status</span></span> <br><span data-ttu-id="689ae-293">接受 = 已接收或傳送正值的功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-293">Accepted = Received or sent a positive functional ack.</span></span> <br><span data-ttu-id="689ae-294">拒絕 = 已接收或傳送負值的功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-294">Rejected = Received or sent a negative functional ack.</span></span> <br><span data-ttu-id="689ae-295">暫止 = 預期要有功能通知但未收到。</span><span class="sxs-lookup"><span data-stu-id="689ae-295">Pending = Expecting a functional ack but not received.</span></span> <br><span data-ttu-id="689ae-296">暫止的 = 產生功能通知，但無法傳送 toopartner。</span><span class="sxs-lookup"><span data-stu-id="689ae-296">Pending = Generated a functional ack but can't send toopartner.</span></span> <br><span data-ttu-id="689ae-297">不需要 = 未設定功能通知。</span><span class="sxs-lookup"><span data-stu-id="689ae-297">Not Required = Functional Ack is not set up.</span></span> |
| <span data-ttu-id="689ae-298">方向</span><span class="sxs-lookup"><span data-stu-id="689ae-298">Direction</span></span> | <span data-ttu-id="689ae-299">hello EDIFACT 訊息方向</span><span class="sxs-lookup"><span data-stu-id="689ae-299">hello EDIFACT message direction</span></span> |
| <span data-ttu-id="689ae-300">相互關連識別碼</span><span class="sxs-lookup"><span data-stu-id="689ae-300">Correlation ID</span></span> | <span data-ttu-id="689ae-301">相互關聯的所有 hello 觸發程序和動作邏輯應用程式中的 hello 識別碼</span><span class="sxs-lookup"><span data-stu-id="689ae-301">hello ID that correlates all hello triggers and actions in a logic app</span></span> |
| <span data-ttu-id="689ae-302">訊息類型</span><span class="sxs-lookup"><span data-stu-id="689ae-302">Msg type</span></span> | <span data-ttu-id="689ae-303">hello EDIFACT 訊息類型</span><span class="sxs-lookup"><span data-stu-id="689ae-303">hello EDIFACT message type</span></span> |
| <span data-ttu-id="689ae-304">ICN</span><span class="sxs-lookup"><span data-stu-id="689ae-304">ICN</span></span> | <span data-ttu-id="689ae-305">hello EDIFACT 訊息的 hello 交換控制編號</span><span class="sxs-lookup"><span data-stu-id="689ae-305">hello Interchange Control Number for hello EDIFACT message</span></span> |
| <span data-ttu-id="689ae-306">TSCN</span><span class="sxs-lookup"><span data-stu-id="689ae-306">TSCN</span></span> | <span data-ttu-id="689ae-307">hello EDIFACT 訊息的交易集控制編號 hello</span><span class="sxs-lookup"><span data-stu-id="689ae-307">hello Transaction Set Control Number for hello EDIFACT message</span></span> |
| <span data-ttu-id="689ae-308">Timestamp</span><span class="sxs-lookup"><span data-stu-id="689ae-308">Timestamp</span></span> | <span data-ttu-id="689ae-309">hello hello EDIFACT 動作處理 hello 訊息時的時間</span><span class="sxs-lookup"><span data-stu-id="689ae-309">hello time when hello EDIFACT action processed hello message</span></span> |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a><span data-ttu-id="689ae-310">所下載訊息檔案的 EDIFACT 名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-310">EDIFACT name formats for downloaded message files</span></span>

<span data-ttu-id="689ae-311">以下是針對每個下載的 EDIFACT 訊息的資料夾和檔案的 hello 名稱格式。</span><span class="sxs-lookup"><span data-stu-id="689ae-311">Here are hello name formats for each downloaded EDIFACT message folder and files.</span></span>

| <span data-ttu-id="689ae-312">資料夾或檔案</span><span class="sxs-lookup"><span data-stu-id="689ae-312">Folder or file</span></span> | <span data-ttu-id="689ae-313">名稱格式</span><span class="sxs-lookup"><span data-stu-id="689ae-313">Name format</span></span> |
| :------------- | :---------- |
| <span data-ttu-id="689ae-314">訊息資料夾</span><span class="sxs-lookup"><span data-stu-id="689ae-314">Message folder</span></span> | <span data-ttu-id="689ae-315">[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_[通用控制編號]\_[交易集控制編號]\_[時間戳記]</span><span class="sxs-lookup"><span data-stu-id="689ae-315">[sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_[global-control-number]\_[transaction-set-control-number]\_[timestamp]</span></span> |
| <span data-ttu-id="689ae-316">輸入、輸出和通知檔案 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="689ae-316">Input, output, and if set up, acknowledgement files</span></span> | <span data-ttu-id="689ae-317">**輸入承載**：[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_input_payload.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-317">**Input payload**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_input_payload.txt</span></span> </p><span data-ttu-id="689ae-318">**輸出承載**：[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_output\_payload.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-318">**Output payload**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_output\_payload.txt</span></span> </p></p><span data-ttu-id="689ae-319">**輸入**：[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_inputs.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-319">**Inputs**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_inputs.txt</span></span> </p></p><span data-ttu-id="689ae-320">**輸出**：[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_outputs.txt</span><span class="sxs-lookup"><span data-stu-id="689ae-320">**Outputs**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_outputs.txt</span></span> |
|          |             |

## <a name="next-steps"></a><span data-ttu-id="689ae-321">後續步驟</span><span class="sxs-lookup"><span data-stu-id="689ae-321">Next steps</span></span>

* [<span data-ttu-id="689ae-322">在 Operations Management Suite 中查詢 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="689ae-322">Query for B2B messages in Operations Management Suite</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [<span data-ttu-id="689ae-323">AS2 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="689ae-323">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="689ae-324">X12 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="689ae-324">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="689ae-325">自訂追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="689ae-325">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)