---
title: "了解如何在 Azure Logic Apps 中使用 MQ 連接器 | Microsoft Docs"
description: "從邏輯應用程式工作流程連線到內部部署或 Azure MQ Server，來瀏覽、接收及傳送訊息至 WebSphere MQ"
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
ms.openlocfilehash: 17c651585b56dae186286f5d8c68c363ae9c524d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-ibm-mq-server-from-logic-apps-using-the-mq-connector"></a><span data-ttu-id="db435-103">使用 MQ 連接器從 Logic Apps 連線到 IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="db435-103">Connect to an IBM MQ server from logic apps using the MQ connector</span></span> 

<span data-ttu-id="db435-104">Microsoft Connector for MQ 會傳送並取出儲存在 MQ Server 內部部署或在 Azure 中的訊息。</span><span class="sxs-lookup"><span data-stu-id="db435-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="db435-105">此連接器包含透過 TCP/IP 網路與遠端 IBM MQ Server 通訊的 Microsoft MQ 用戶端。</span><span class="sxs-lookup"><span data-stu-id="db435-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="db435-106">本文件是使用 MQ 連接器的入門指南。</span><span class="sxs-lookup"><span data-stu-id="db435-106">This document is a starter guide to use the MQ connector.</span></span> <span data-ttu-id="db435-107">建議您從瀏覽佇列上的單一訊息開始，然後再嘗試其他動作。</span><span class="sxs-lookup"><span data-stu-id="db435-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span></span>    

<span data-ttu-id="db435-108">MQ 連接器包含下列動作。</span><span class="sxs-lookup"><span data-stu-id="db435-108">The MQ connector includes the following actions.</span></span> <span data-ttu-id="db435-109">但不包含觸發程序。</span><span class="sxs-lookup"><span data-stu-id="db435-109">There are no triggers.</span></span>

-   <span data-ttu-id="db435-110">瀏覽單一訊息，而不從 IBM MQ Server 刪除訊息</span><span class="sxs-lookup"><span data-stu-id="db435-110">Browse a single message without deleting the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="db435-111">瀏覽批次訊息，而不從 IBM MQ Server 刪除訊息</span><span class="sxs-lookup"><span data-stu-id="db435-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="db435-112">接收單一訊息，並從 IBM MQ Server 刪除訊息</span><span class="sxs-lookup"><span data-stu-id="db435-112">Receive a single message and delete the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="db435-113">接收批次訊息，並從 IBM MQ Server 刪除訊息</span><span class="sxs-lookup"><span data-stu-id="db435-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="db435-114">將單一訊息傳送至 IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="db435-114">Send a single message to the IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db435-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="db435-115">Prerequisites</span></span>

* <span data-ttu-id="db435-116">如果是使用內部部署 MQ Server，請在網路內之伺服器上[安裝內部部署資料閘道](../logic-apps/logic-apps-gateway-install.md)。</span><span class="sxs-lookup"><span data-stu-id="db435-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="db435-117">如果 MQ Server 可公開使用或可在 Azure 內使用，就是沒有使用資料閘道或不需要資料閘道。</span><span class="sxs-lookup"><span data-stu-id="db435-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="db435-118">安裝內部部署資料閘道的伺服器也必須安裝適用於 MQ 連接器的 .Net Framework 4.6 才能運作。</span><span class="sxs-lookup"><span data-stu-id="db435-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span></span>

* <span data-ttu-id="db435-119">建立內部部署資料閘道的 Azure 資源 - [設定資料閘道連線](../logic-apps/logic-apps-gateway-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="db435-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="db435-120">正式支援的 IBM WebSphere MQ 版本：</span><span class="sxs-lookup"><span data-stu-id="db435-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="db435-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="db435-121">MQ 7.5</span></span>
   * <span data-ttu-id="db435-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="db435-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="db435-123">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="db435-123">Create a logic app</span></span>

1. <span data-ttu-id="db435-124">在 **Azure 開始面板**中，依序選取 **+** (加號)、[Web + 行動] 和 [邏輯應用程式]。</span><span class="sxs-lookup"><span data-stu-id="db435-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="db435-125">輸入 [名稱]，例如 MQTestApp、[訂用帳戶]、[資源群組]，和 [位置](使用已設定內部部署資料閘道連線的位置)。</span><span class="sxs-lookup"><span data-stu-id="db435-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="db435-126">選取 [釘選到儀表板]，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="db435-126">Select **Pin to dashboard**, and select **Create**.</span></span>  
<span data-ttu-id="db435-127">![建立邏輯應用程式](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="db435-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="db435-128">新增觸發程序</span><span class="sxs-lookup"><span data-stu-id="db435-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="db435-129">MQ 連接器並沒有任何觸發程序。</span><span class="sxs-lookup"><span data-stu-id="db435-129">The MQ Connector does not have any triggers.</span></span> <span data-ttu-id="db435-130">因此，使用另一個觸發程序來啟動邏輯應用程式，例如 [定期] 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="db435-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="db435-131">**Logic Apps Designer** 隨即開啟，在一般觸發程序的清單中選取 [定期]。</span><span class="sxs-lookup"><span data-stu-id="db435-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span></span>
2. <span data-ttu-id="db435-132">在定期觸發程序內選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="db435-132">Select **Edit** within the Recurrence Trigger.</span></span> 
3. <span data-ttu-id="db435-133">將 [頻率] 設定為 [天]，將 [間隔] 設定為 **7**。</span><span class="sxs-lookup"><span data-stu-id="db435-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="db435-134">瀏覽單一訊息</span><span class="sxs-lookup"><span data-stu-id="db435-134">Browse a single message</span></span>
1. <span data-ttu-id="db435-135">選取 [+ 新增步驟]，再選取 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="db435-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="db435-136">在 [搜尋] 方塊中，輸入 `mq`，然後選取 [MQ - 瀏覽訊息]。</span><span class="sxs-lookup"><span data-stu-id="db435-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="db435-137">![瀏覽訊息](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="db435-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="db435-138">如果沒有現有的 MQ 連線，就建立連線：</span><span class="sxs-lookup"><span data-stu-id="db435-138">If there isn't an existing MQ connection, then create the connection:</span></span>  

    1. <span data-ttu-id="db435-139">選取 [透過內部部署資料閘道連線]，並輸入 MQ Server 的屬性。</span><span class="sxs-lookup"><span data-stu-id="db435-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span></span>  
    <span data-ttu-id="db435-140">針對 [伺服器]，您可以輸入 MQ Server 的名稱，或輸入 IP 位址，後面接著冒號和連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="db435-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span></span> 
    2. <span data-ttu-id="db435-141">[閘道] 下拉式清單中會列出已設定的任何現有閘道連線。</span><span class="sxs-lookup"><span data-stu-id="db435-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="db435-142">選取您的閘道。</span><span class="sxs-lookup"><span data-stu-id="db435-142">Select your gateway.</span></span>
    3. <span data-ttu-id="db435-143">完成後，請選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="db435-143">Select **Create** when finished.</span></span> <span data-ttu-id="db435-144">連線看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="db435-144">Your connection looks similar to the following:</span></span>   
    <span data-ttu-id="db435-145">![連線屬性](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="db435-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="db435-146">在動作屬性中，您可以：</span><span class="sxs-lookup"><span data-stu-id="db435-146">In the action properties, you can:</span></span>  

    * <span data-ttu-id="db435-147">使用 **Queue** 屬性來存取與連線中所定義不同的佇列名稱</span><span class="sxs-lookup"><span data-stu-id="db435-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span></span>
    * <span data-ttu-id="db435-148">使用 **MessageId**、**CorrelationId**、**GroupId** 和其他屬性，來瀏覽以不同 MQ 訊息屬性作為基礎的訊息</span><span class="sxs-lookup"><span data-stu-id="db435-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span></span>
    * <span data-ttu-id="db435-149">將 **IncludeInfo** 設定為 **True**，可在輸出中包含額外的訊息資訊。</span><span class="sxs-lookup"><span data-stu-id="db435-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span></span> <span data-ttu-id="db435-150">或者，將它設定為 **False**，可在輸出中排除額外的訊息資訊。</span><span class="sxs-lookup"><span data-stu-id="db435-150">Or, set it to **False** to not include additional message information in the output.</span></span>
    * <span data-ttu-id="db435-151">輸入 [逾時] 值，來決定訊息到達空白查詢中的等候時間。</span><span class="sxs-lookup"><span data-stu-id="db435-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span></span> <span data-ttu-id="db435-152">如果未輸入任何內容，就會取出佇列中的第一個訊息，且不會花費時間等候要顯示的訊息。</span><span class="sxs-lookup"><span data-stu-id="db435-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span></span>  
    <span data-ttu-id="db435-153">![瀏覽訊息屬性](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="db435-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="db435-154">[儲存] 您的變更，然後 [執行] 邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="db435-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="db435-155">![儲存並執行](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="db435-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="db435-156">幾秒之後，會顯示執行的步驟，且您可以查看輸出。</span><span class="sxs-lookup"><span data-stu-id="db435-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span></span> <span data-ttu-id="db435-157">選擇綠色核取記號可查看每個步驟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="db435-157">Select the green checkmark to see details of each step.</span></span> <span data-ttu-id="db435-158">選取 [查看原始輸出] 可查看輸出資料上的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="db435-158">Select **See raw outputs** to see additional details on the output data.</span></span>  
<span data-ttu-id="db435-159">![瀏覽訊息輸出](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="db435-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="db435-160">原始輸出：</span><span class="sxs-lookup"><span data-stu-id="db435-160">Raw output:</span></span>  
    ![瀏覽訊息原始輸出](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="db435-162">當 **IncludeInfo** 選項設定為 true 時，會顯示下列輸出：</span><span class="sxs-lookup"><span data-stu-id="db435-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span></span>  
<span data-ttu-id="db435-163">![瀏覽訊息包含資訊](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="db435-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="db435-164">瀏覽多個訊息</span><span class="sxs-lookup"><span data-stu-id="db435-164">Browse multiple messages</span></span>
<span data-ttu-id="db435-165">[瀏覽訊息] 動作包含 **BatchSize** 選項，指出應該從佇列傳回的訊息數量。</span><span class="sxs-lookup"><span data-stu-id="db435-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span></span>  <span data-ttu-id="db435-166">如果 **BatchSize** 沒有項目，就會傳回所有的訊息。</span><span class="sxs-lookup"><span data-stu-id="db435-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="db435-167">傳回的輸出是陣列訊息。</span><span class="sxs-lookup"><span data-stu-id="db435-167">The returned output is an array of messages.</span></span>

1. <span data-ttu-id="db435-168">新增 [瀏覽訊息] 動作時，預設會選取所設定的第一個連線。</span><span class="sxs-lookup"><span data-stu-id="db435-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="db435-169">選取 [變更連線] 來建立新的連線，或選取不同的連線。</span><span class="sxs-lookup"><span data-stu-id="db435-169">Select **Change connection** to create a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="db435-170">瀏覽訊息的輸出會顯示：</span><span class="sxs-lookup"><span data-stu-id="db435-170">The output of Browse messages shows:</span></span>  
![瀏覽訊息輸出](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="db435-172">接收單一訊息</span><span class="sxs-lookup"><span data-stu-id="db435-172">Receive a single message</span></span>
<span data-ttu-id="db435-173">[接收訊息] 動作具有與 [瀏覽訊息] 動作相同的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="db435-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span></span> <span data-ttu-id="db435-174">使用 [接收訊息] 時，會從佇列將訊息刪除。</span><span class="sxs-lookup"><span data-stu-id="db435-174">When using **Receive message**, the message is deleted from the queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="db435-175">接收多個訊息</span><span class="sxs-lookup"><span data-stu-id="db435-175">Receive multiple messages</span></span>
<span data-ttu-id="db435-176">[接收訊息] 動作具有與 [瀏覽訊息] 動作相同的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="db435-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span></span> <span data-ttu-id="db435-177">使用 [接收訊息] 時，會從佇列將訊息刪除。</span><span class="sxs-lookup"><span data-stu-id="db435-177">When using **Receive messages**, the messages are deleted from the queue.</span></span>

<span data-ttu-id="db435-178">如果進行瀏覽或接收時佇列中沒有任何訊息，步驟就會失敗，並出現下列輸出：</span><span class="sxs-lookup"><span data-stu-id="db435-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span></span>  
![MQ 無訊息錯誤](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="db435-180">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="db435-180">Send a message</span></span>
1. <span data-ttu-id="db435-181">新增 [傳送訊息] 動作時，預設會選取所設定的第一個連線。</span><span class="sxs-lookup"><span data-stu-id="db435-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="db435-182">選取 [變更連線] 來建立新的連線，或選取不同的連線。</span><span class="sxs-lookup"><span data-stu-id="db435-182">Select **Change connection** to create a new connection, or select a different connection.</span></span> <span data-ttu-id="db435-183">有效的 [訊息類型] 是 [資料包]、[回覆] 或 [要求]。</span><span class="sxs-lookup"><span data-stu-id="db435-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="db435-184">![傳送訊息屬性](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="db435-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="db435-185">傳送訊息的輸出顯示如下：</span><span class="sxs-lookup"><span data-stu-id="db435-185">The output of Send message looks like the following:</span></span>  
![傳送訊息輸出](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="db435-187">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="db435-187">Connector-specific details</span></span>

<span data-ttu-id="db435-188">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/mq/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="db435-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db435-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db435-189">Next steps</span></span>
<span data-ttu-id="db435-190">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="db435-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="db435-191">請到我們的 [API 清單](apis-list.md)探索 Logic Apps 中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="db435-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
