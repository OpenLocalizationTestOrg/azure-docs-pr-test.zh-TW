---
title: "在您的 Azure Logic Apps 中新增 Oracle Database 連接器 | Microsoft Docs"
description: "在邏輯應用程式中使用 Oracle Database 連接器"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: cc64441617eb5e7d5e70c1cf5c491a672428bc51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-the-oracle-database-connector"></a><span data-ttu-id="0cbe3-103">開始使用 Oracle Database 連接器</span><span class="sxs-lookup"><span data-stu-id="0cbe3-103">Get started with the Oracle Database connector</span></span>

<span data-ttu-id="0cbe3-104">透過 Oracle Database 連接器，您可以使用現有資料庫中的資料來建立組織工作流程。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-104">Using the Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="0cbe3-105">此連接器可以連線至內部部署 Oracle Database，或是已安裝 Oracle Database 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-105">This connector can connect to an on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="0cbe3-106">您可以使用此連接器來：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-106">With this connector, you can:</span></span>

* <span data-ttu-id="0cbe3-107">藉由在客戶資料庫中新增新客戶或在訂單資料庫中更新訂單，以建置工作流程。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-107">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="0cbe3-108">使用動作來取得一列資料、插入新的資料列，甚至加以刪除。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-108">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="0cbe3-109">例如，在 Dynamics CRM Online 中建立記錄時 (觸發程序)，就會在 Oracle Database 中插入資料列 (動作)。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="0cbe3-110">本主題說明如何在邏輯應用程式中使用 Oracle Database 連接器。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-110">This topic shows you how to use the Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cbe3-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="0cbe3-111">Prerequisites</span></span>

* <span data-ttu-id="0cbe3-112">支援的 Oracle 版本：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="0cbe3-113">Oracle 9 和更新版本</span><span class="sxs-lookup"><span data-stu-id="0cbe3-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="0cbe3-114">Oracle 用戶端軟體 8.1.7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="0cbe3-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="0cbe3-115">安裝內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-115">Install the on-premises data gateway.</span></span> <span data-ttu-id="0cbe3-116">[從邏輯應用程式連線至內部部署資料](../logic-apps/logic-apps-gateway-connection.md)中會列出相關步驟。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-116">[Connect to on-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists the steps.</span></span> <span data-ttu-id="0cbe3-117">您需要閘道或是已安裝 Oracle DB 的 Azure VM，才能連線至內部部署 Oracle Database。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-117">The gateway is required to connect to an on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="0cbe3-118">內部部署資料閘道的角色如同橋接器，在內部部署資料 (不在雲端中的資料) 和邏輯應用程式之間提供安全的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-118">The on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in the cloud) and your logic apps.</span></span> <span data-ttu-id="0cbe3-119">相同的閘道可以與多個服務，以及多個資料來源搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-119">The same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="0cbe3-120">因此，您只需要安裝一次閘道即可。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-120">So, you may only need to install the gateway once.</span></span>

* <span data-ttu-id="0cbe3-121">在您安裝內部部署資料閘道的機器上安裝 Oracle Client。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-121">Install the Oracle Client on the machine where you installed the on-premises data gateway.</span></span> <span data-ttu-id="0cbe3-122">請務必從 Oracle 安裝 64 位元的 Oracle Data Provider for .NET：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-122">Be sure to install the 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="0cbe3-123">適用於 Windows x64 的 64 位元 ODAC 12c 版本 4 (12.1.0.2.4)</span><span class="sxs-lookup"><span data-stu-id="0cbe3-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="0cbe3-124">若未安裝 Oracle 用戶端，當您嘗試建立或使用連線時會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-124">If the Oracle client is not installed, an error occurs when you try to create or use the connection.</span></span> <span data-ttu-id="0cbe3-125">請參閱本主題中常見的錯誤。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-125">See the common errors in this topic.</span></span>


## <a name="add-the-connector"></a><span data-ttu-id="0cbe3-126">新增連接器</span><span class="sxs-lookup"><span data-stu-id="0cbe3-126">Add the connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0cbe3-127">此連接器並沒有任何觸發程序。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-127">This connector does not have any triggers.</span></span> <span data-ttu-id="0cbe3-128">只有動作。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-128">It has only actions.</span></span> <span data-ttu-id="0cbe3-129">因此，當您建立邏輯應用程式時，請新增其他觸發程序以啟動您的邏輯應用程式，例如**排程 - 循環**或**要求/回應 - 回應**。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-129">So when you create your logic app, add another trigger to start your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="0cbe3-130">在 [Azure 入口網站](https://portal.azure.com) 中，建立空白的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-130">In the [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="0cbe3-131">在邏輯應用程式啟動時，選取**要求/回應 - 要求**觸發程序：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-131">At the start of your logic app, select the **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="0cbe3-132">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-132">Select **Save**.</span></span> <span data-ttu-id="0cbe3-133">當您儲存時，系統會自動生產生一個要求 URL。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="0cbe3-134">選取 [新增步驟]，再選取 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="0cbe3-135">輸入 `oracle` 以查看可用的動作：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-135">Type in `oracle` to see the available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="0cbe3-136">這也是查看連接器可使用的觸發程序和動作最快的方法。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-136">This is also the quickest way to see the triggers and actions available for any connector.</span></span> <span data-ttu-id="0cbe3-137">輸入連接器的部分名稱，例如 `oracle`。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-137">Type in part of the connector name, such as `oracle`.</span></span> <span data-ttu-id="0cbe3-138">設計工具會列出所有觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-138">The designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="0cbe3-139">選取其中一個動作，例如 [Oracle Database - 立即取得]。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-139">Select one of the actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="0cbe3-140">選取 [透過內部部署資料閘道連線]。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="0cbe3-141">輸入 Oracle 伺服器名稱、驗證方法、使用者名稱、密碼並選取閘道：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-141">Enter the Oracle server name, authentication method, username, password, and select the gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="0cbe3-142">連線之後，從清單中選取資料表，接著輸入資料表的資料列識別碼。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-142">Once connected, select a table from the list, and enter the row ID to your table.</span></span> <span data-ttu-id="0cbe3-143">您必須知道資料表的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-143">You need to know the identifier to the table.</span></span> <span data-ttu-id="0cbe3-144">如果您不知道，請連絡 Oracle DB 管理員，並從 `select * from yourTableName` 取得輸出資料。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-144">If you don't know, contact your Oracle DB administrator, and get the output from `select * from yourTableName`.</span></span> <span data-ttu-id="0cbe3-145">這可讓您取得必要的可識別資料以繼續作業。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-145">This gives you the identifiable information you need to proceed.</span></span>

    <span data-ttu-id="0cbe3-146">在下列範例中，會從人力資源資料庫中傳回作業資料：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-146">In the following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="0cbe3-147">在下一個步驟中，您可以使用其他任何連接器來建置您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-147">In this next step, you can use any of the other connectors to build your workflow.</span></span> <span data-ttu-id="0cbe3-148">若您想測試從 Oracle 取得資料，請使用其中一個寄送電子郵件連接器 (例如 Office 365 或 Gmail)，將包含 Oracle 資料的電子郵件寄給自己。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-148">If you want to test getting data from Oracle, then send yourself an email with the Oracle data using one of the send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="0cbe3-149">使用 Oracle 資料表中的動態權杖來建置`Subject`以及您電子郵件的 `Body`：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-149">Use the dynamic tokens from the Oracle table to build the `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="0cbe3-150">**儲存**您的邏輯應用程式，接著選取 [執行]。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="0cbe3-151">關閉設計工具，接著查看狀態的執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-151">Close the designer, and look at the runs history for the status.</span></span> <span data-ttu-id="0cbe3-152">如果失敗，請選取失敗的訊息資料列。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-152">If it fails, select the failed message row.</span></span> <span data-ttu-id="0cbe3-153">設計工具隨即開啟，並顯示失敗的步驟，以及錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-153">The designer opens, and shows you which step failed, and also shows the error information.</span></span> <span data-ttu-id="0cbe3-154">如果成功，您應該會收到一封電子郵件，內含您新增的資訊。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-154">If it succeeds, then you should receive an email with the information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="0cbe3-155">工作流程想法</span><span class="sxs-lookup"><span data-stu-id="0cbe3-155">Workflow ideas</span></span>

* <span data-ttu-id="0cbe3-156">您希望能監視 #oracle 主題標籤，並在資料庫中放置推文以便查詢，並在其他應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-156">You want to monitor the #oracle hashtag, and put the tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="0cbe3-157">在邏輯應用程式中，新增 `Twitter - When a new tweet is posted` 觸發程序並輸入 **#oracle** 主題標籤。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-157">In a logic app, add the `Twitter - When a new tweet is posted` trigger, and enter the **#oracle** hashtag.</span></span> <span data-ttu-id="0cbe3-158">接著，新增 `Oracle Database - Insert row` 動作，再選取您的資料表：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-158">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="0cbe3-159">訊息已傳送至服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-159">Messages are sent to a Service Bus queue.</span></span> <span data-ttu-id="0cbe3-160">您希望取得這些訊息，並將其放在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-160">You want to get these messages, and put them in a database.</span></span> <span data-ttu-id="0cbe3-161">在邏輯應用程式中，新增 `Service Bus - when a message is received in a queue` 觸發程序，並選取該佇列。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-161">In a logic app, add the `Service Bus - when a message is received in a queue` trigger, and select the queue.</span></span> <span data-ttu-id="0cbe3-162">接著，新增 `Oracle Database - Insert row` 動作，再選取您的資料表：</span><span class="sxs-lookup"><span data-stu-id="0cbe3-162">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="0cbe3-163">常見錯誤</span><span class="sxs-lookup"><span data-stu-id="0cbe3-163">Common errors</span></span>

#### <a name="error-cannot-reach-the-gateway"></a><span data-ttu-id="0cbe3-164">**錯誤**：無法連線至閘道</span><span class="sxs-lookup"><span data-stu-id="0cbe3-164">**Error**: Cannot reach the Gateway</span></span>

<span data-ttu-id="0cbe3-165">**原因**：內部部署資料閘道無法連線至雲端。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-165">**Cause**: The on-premises data gateway is not able to connect to the cloud.</span></span> 

<span data-ttu-id="0cbe3-166">**風險降低**：確保您的閘道在安裝的內部部署機器中執行，且可連線至網際網路。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-166">**Mitigation**: Make sure your gateway is running on the on-premises machine where you installed it, and that it can connect to the internet.</span></span>  <span data-ttu-id="0cbe3-167">我們建議不要在可能關閉或休眠的電腦上安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-167">We recommend not installing the gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="0cbe3-168">您也可以重新啟動內部部署資料閘道服務 (PBIEgwService)。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-168">You can also restart the on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-the-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-to-install-the-official-provider"></a><span data-ttu-id="0cbe3-169">**錯誤**：使用的提供者已被取代：'System.Data.OracleClient requires Oracle 用戶端軟體版本 8.1.7 或更高版本。'。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-169">**Error**: The provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="0cbe3-170">請造訪 [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) 以安裝正式的提供者。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) to install the official provider.</span></span>

<span data-ttu-id="0cbe3-171">**原因**：Oracle 用戶端 SDK 並未安裝在內部部署資料閘道執行的機器上。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-171">**Cause**: The Oracle client SDK is not installed on the machine where the on-premises data gateway is running.</span></span>  

<span data-ttu-id="0cbe3-172">**解決方案**：在與內部部署資料閘道相同的電腦上下載並安裝 Oracle 用戶端 SDK。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-172">**Resolution**: Download and install the Oracle client SDK on the same computer as the on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="0cbe3-173">**錯誤**：資料表 '[Tablename]' 並未定義任何索引鍵資料行</span><span class="sxs-lookup"><span data-stu-id="0cbe3-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="0cbe3-174">**原因**：資料表沒有任何主要索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-174">**Cause**: The table does not have any primary key.</span></span>  

<span data-ttu-id="0cbe3-175">**解決方案**：Oracle Database 連接器需要使用主要索引鍵資料行的資料表。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-175">**Resolution**: The Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="0cbe3-176">目前不支援</span><span class="sxs-lookup"><span data-stu-id="0cbe3-176">Currently not supported</span></span>

* <span data-ttu-id="0cbe3-177">檢視和已存程序</span><span class="sxs-lookup"><span data-stu-id="0cbe3-177">Views and stored procedures</span></span> 
* <span data-ttu-id="0cbe3-178">包含複合索引鍵的任何資料表</span><span class="sxs-lookup"><span data-stu-id="0cbe3-178">Any table with composite keys</span></span>
* <span data-ttu-id="0cbe3-179">資料表中的巢狀物件類型</span><span class="sxs-lookup"><span data-stu-id="0cbe3-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="0cbe3-180">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="0cbe3-180">Connector-specific details</span></span>

<span data-ttu-id="0cbe3-181">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/oracle/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-181">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="0cbe3-182">取得協助</span><span class="sxs-lookup"><span data-stu-id="0cbe3-182">Get some help</span></span>

<span data-ttu-id="0cbe3-183">若要提出問題、回答問題以及查看其他 Logic Apps 使用者的做法，可以前往 [Azure Logic Apps 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-183">The [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place to ask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="0cbe3-184">您可以投票並在 [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish) 中提交意見，協助改善 Logic Apps 和連接器。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="0cbe3-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0cbe3-185">Next steps</span></span>
<span data-ttu-id="0cbe3-186">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)，並到我們的 [API 清單](apis-list.md)探索 Logic Apps 中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="0cbe3-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore the available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
