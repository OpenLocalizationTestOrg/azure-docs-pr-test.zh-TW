---
title: "aaaLearn toouse hello Azure 邏輯應用程式中的 MQ 連接器的方式 |Microsoft 文件"
description: "從您的邏輯應用程式工作流程 toobrowse 連接 tooan 內部部署或 Azure MQ 伺服器、 接收和傳送訊息 tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="b67fa-103">從邏輯應用程式使用 hello MQ 連接器連接 tooan IBM MQ 伺服器</span><span class="sxs-lookup"><span data-stu-id="b67fa-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="b67fa-104">Microsoft Connector for MQ 會傳送並取出儲存在 MQ Server 內部部署或在 Azure 中的訊息。</span><span class="sxs-lookup"><span data-stu-id="b67fa-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="b67fa-105">此連接器包含透過 TCP/IP 網路與遠端 IBM MQ Server 通訊的 Microsoft MQ 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b67fa-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="b67fa-106">這份文件是入門指南 toouse hello MQ 連接器。</span><span class="sxs-lookup"><span data-stu-id="b67fa-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="b67fa-107">我們建議您開始瀏覽到佇列中，單一訊息，然後嘗試 hello 其他動作。</span><span class="sxs-lookup"><span data-stu-id="b67fa-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="b67fa-108">hello MQ 連接器包括下列動作的 hello。</span><span class="sxs-lookup"><span data-stu-id="b67fa-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="b67fa-109">但不包含觸發程序。</span><span class="sxs-lookup"><span data-stu-id="b67fa-109">There are no triggers.</span></span>

-   <span data-ttu-id="b67fa-110">瀏覽單一訊息，而不從 hello IBM MQ Server 刪除 hello 訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="b67fa-111">瀏覽訊息批次，但不會刪除從 hello IBM MQ 伺服器 hello 訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="b67fa-112">接收單一訊息，並從 hello IBM MQ Server 刪除 hello 訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="b67fa-113">接收的訊息批次，並從 hello IBM MQ Server 刪除 hello 訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="b67fa-114">傳送單一訊息 toohello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="b67fa-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b67fa-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="b67fa-115">Prerequisites</span></span>

* <span data-ttu-id="b67fa-116">如果使用內部部署 MQ server 上，[安裝 hello 在內部部署資料閘道](../logic-apps/logic-apps-gateway-install.md)網路內之伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b67fa-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="b67fa-117">如果 hello MQ Server 上公開使用，或在 Azure 中可用，然後 hello data gateway 已無法使用或所需。</span><span class="sxs-lookup"><span data-stu-id="b67fa-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b67fa-118">hello 伺服器其中 hello 安裝在內部部署資料閘道也必須有.Net Framework 4.6 安裝 hello MQ 連接器 toofunction。</span><span class="sxs-lookup"><span data-stu-id="b67fa-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="b67fa-119">建立 Azure 資源 hello 在內部部署資料閘道-hello [hello 資料閘道連接設定](../logic-apps/logic-apps-gateway-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="b67fa-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="b67fa-120">正式支援的 IBM WebSphere MQ 版本：</span><span class="sxs-lookup"><span data-stu-id="b67fa-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="b67fa-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="b67fa-121">MQ 7.5</span></span>
   * <span data-ttu-id="b67fa-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="b67fa-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="b67fa-123">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b67fa-123">Create a logic app</span></span>

1. <span data-ttu-id="b67fa-124">在 hello **Azure 開始面板**，選取 **+**  （加號） **Web + 行動**，，然後**邏輯應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b67fa-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="b67fa-125">輸入 hello**名稱**，例如 MQTestApp，**訂用帳戶**，**資源群組**，和**位置**（使用 hello 位置，其中 hello在內部部署資料閘道連線已設定）。</span><span class="sxs-lookup"><span data-stu-id="b67fa-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="b67fa-126">選取**Pin toodashboard**，然後選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="b67fa-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="b67fa-127">![建立邏輯應用程式](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="b67fa-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="b67fa-128">新增觸發程序</span><span class="sxs-lookup"><span data-stu-id="b67fa-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="b67fa-129">hello MQ 連接器並沒有任何觸發程序。</span><span class="sxs-lookup"><span data-stu-id="b67fa-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="b67fa-130">因此，使用另一個觸發程序 toostart 邏輯應用程式，例如 hello**循環**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="b67fa-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="b67fa-131">hello**邏輯應用程式設計師**隨即開啟，選取**循環**hello 一般的觸發程序清單中。</span><span class="sxs-lookup"><span data-stu-id="b67fa-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="b67fa-132">選取**編輯**hello 循環觸發程序內。</span><span class="sxs-lookup"><span data-stu-id="b67fa-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="b67fa-133">設定 hello**頻率**太**天**，和集合 hello**間隔**太**7**。</span><span class="sxs-lookup"><span data-stu-id="b67fa-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="b67fa-134">瀏覽單一訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-134">Browse a single message</span></span>
1. <span data-ttu-id="b67fa-135">選取 [+ 新增步驟]，再選取 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="b67fa-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="b67fa-136">在 [hello] 搜尋方塊中，輸入`mq`，然後選取**MQ-瀏覽訊息**。</span><span class="sxs-lookup"><span data-stu-id="b67fa-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="b67fa-137">![瀏覽訊息](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="b67fa-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="b67fa-138">如果沒有現有的 MQ 連接，然後建立 hello 連線：</span><span class="sxs-lookup"><span data-stu-id="b67fa-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="b67fa-139">選取**連接透過內部部署資料閘道**，然後輸入 hello MQ 伺服器屬性。</span><span class="sxs-lookup"><span data-stu-id="b67fa-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="b67fa-140">如**伺服器**，您可以輸入 hello MQ 的伺服器名稱，或輸入 hello IP 位址，後面接著冒號和 hello 的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="b67fa-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="b67fa-141">hello**閘道**下拉式清單中列出的任何現有的閘道連線已設定。</span><span class="sxs-lookup"><span data-stu-id="b67fa-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="b67fa-142">選取您的閘道。</span><span class="sxs-lookup"><span data-stu-id="b67fa-142">Select your gateway.</span></span>
    3. <span data-ttu-id="b67fa-143">完成後，請選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b67fa-143">Select **Create** when finished.</span></span> <span data-ttu-id="b67fa-144">您的連線看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="b67fa-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="b67fa-145">![連線屬性](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="b67fa-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="b67fa-146">在 hello 動作屬性，您可以：</span><span class="sxs-lookup"><span data-stu-id="b67fa-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="b67fa-147">使用 hello**佇列**屬性 tooaccess 比 hello 連接中所定義不同的佇列名稱</span><span class="sxs-lookup"><span data-stu-id="b67fa-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="b67fa-148">使用 hello **MessageId**， **CorrelationId**， **GroupId**，和其他的屬性 toobrowse hello 不同 MQ 訊息屬性為基礎的訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="b67fa-149">設定**IncludeInfo**太**True** tooinclude hello 輸出中的其他訊息資訊。</span><span class="sxs-lookup"><span data-stu-id="b67fa-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="b67fa-150">或者，您也可以設定得**False** toonot hello 輸出中包含額外的訊息資訊。</span><span class="sxs-lookup"><span data-stu-id="b67fa-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="b67fa-151">輸入**逾時**toodetermine 值為空的佇列中訊息 tooarrive 多久 toowait。</span><span class="sxs-lookup"><span data-stu-id="b67fa-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="b67fa-152">如果輸入任何內容，擷取 hello hello 佇列中的第一個訊息，並沒有時間花在等待訊息 tooappear。</span><span class="sxs-lookup"><span data-stu-id="b67fa-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="b67fa-153">![瀏覽訊息屬性](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="b67fa-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="b67fa-154">[儲存] 您的變更，然後 [執行] 邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="b67fa-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="b67fa-155">![儲存並執行](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="b67fa-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="b67fa-156">幾秒之後，執行 hello hello 步驟會顯示，而且您可以查看 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="b67fa-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="b67fa-157">選取每個步驟的 hello 綠色核取記號 toosee 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b67fa-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="b67fa-158">選取**看到原始輸出**toosee hello 的其他詳細資料輸出資料。</span><span class="sxs-lookup"><span data-stu-id="b67fa-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="b67fa-159">![瀏覽訊息輸出](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="b67fa-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="b67fa-160">原始輸出：</span><span class="sxs-lookup"><span data-stu-id="b67fa-160">Raw output:</span></span>  
    ![瀏覽訊息原始輸出](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="b67fa-162">當 hello **IncludeInfo** tootrue 設定選項時，會顯示下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="b67fa-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="b67fa-163">![瀏覽訊息包含資訊](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="b67fa-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="b67fa-164">瀏覽多個訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-164">Browse multiple messages</span></span>
<span data-ttu-id="b67fa-165">hello**瀏覽訊息**動作包含**BatchSize**選項 tooindicate 應該從 hello 佇列傳回的訊息數量。</span><span class="sxs-lookup"><span data-stu-id="b67fa-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="b67fa-166">如果 **BatchSize** 沒有項目，就會傳回所有的訊息。</span><span class="sxs-lookup"><span data-stu-id="b67fa-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="b67fa-167">hello 傳回輸出的訊息陣列。</span><span class="sxs-lookup"><span data-stu-id="b67fa-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="b67fa-168">當加入 hello**瀏覽訊息**hello 第一個連接所設定的動作，依預設會選取。</span><span class="sxs-lookup"><span data-stu-id="b67fa-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="b67fa-169">選取**變更連接**toocreate 新的連接，或選取不同的連接。</span><span class="sxs-lookup"><span data-stu-id="b67fa-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="b67fa-170">若要瀏覽 hello 輸出訊息所示：</span><span class="sxs-lookup"><span data-stu-id="b67fa-170">hello output of Browse messages shows:</span></span>  
![瀏覽訊息輸出](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="b67fa-172">接收單一訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-172">Receive a single message</span></span>
<span data-ttu-id="b67fa-173">hello**接收訊息**動作已為 hello hello 相同輸入和輸出**瀏覽訊息**動作。</span><span class="sxs-lookup"><span data-stu-id="b67fa-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="b67fa-174">當使用**接收訊息**，hello 訊息從 hello 佇列中刪除。</span><span class="sxs-lookup"><span data-stu-id="b67fa-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="b67fa-175">接收多個訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-175">Receive multiple messages</span></span>
<span data-ttu-id="b67fa-176">hello**接收訊息**動作已為 hello hello 相同輸入和輸出**瀏覽訊息**動作。</span><span class="sxs-lookup"><span data-stu-id="b67fa-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="b67fa-177">當使用**接收訊息**，hello 訊息會從 hello 佇列中刪除。</span><span class="sxs-lookup"><span data-stu-id="b67fa-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="b67fa-178">如果有任何訊息 hello 佇列中進行瀏覽 」 或 「 接收時，hello 步驟失敗 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="b67fa-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![MQ 無訊息錯誤](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="b67fa-180">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="b67fa-180">Send a message</span></span>
1. <span data-ttu-id="b67fa-181">當加入 hello**傳送訊息**hello 第一個連接所設定的動作，依預設會選取。</span><span class="sxs-lookup"><span data-stu-id="b67fa-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="b67fa-182">選取**變更連接**toocreate 新的連接，或選取不同的連接。</span><span class="sxs-lookup"><span data-stu-id="b67fa-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="b67fa-183">有效的 hello**訊息類型**是**資料包**，**回覆**，或**要求**。</span><span class="sxs-lookup"><span data-stu-id="b67fa-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="b67fa-184">![傳送訊息屬性](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="b67fa-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="b67fa-185">hello 傳送訊息的輸出看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="b67fa-185">hello output of Send message looks like hello following:</span></span>  
![傳送訊息輸出](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="b67fa-187">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="b67fa-187">Connector-specific details</span></span>

<span data-ttu-id="b67fa-188">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/mq/)。</span><span class="sxs-lookup"><span data-stu-id="b67fa-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b67fa-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b67fa-189">Next steps</span></span>
<span data-ttu-id="b67fa-190">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="b67fa-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="b67fa-191">瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="b67fa-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
