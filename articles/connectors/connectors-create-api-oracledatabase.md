---
title: "Azure 邏輯應用程式中的 aaaAdd hello Oracle 資料庫連接器 |Microsoft 文件"
description: "在邏輯應用程式中使用 hello Oracle 資料庫連接器"
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
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="6a10e-103">開始使用 hello Oracle 資料庫連接器</span><span class="sxs-lookup"><span data-stu-id="6a10e-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="6a10e-104">使用 hello Oracle 資料庫連接器，您建立組織中現有的資料庫使用資料的工作流程。</span><span class="sxs-lookup"><span data-stu-id="6a10e-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="6a10e-105">此連接器可以連線的 tooan 安裝在內部部署 Oracle 資料庫或 Azure 虛擬機器與 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6a10e-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="6a10e-106">您可以使用此連接器來：</span><span class="sxs-lookup"><span data-stu-id="6a10e-106">With this connector, you can:</span></span>

* <span data-ttu-id="6a10e-107">建置您的工作流程加入新的客戶 tooa 客戶資料庫，或更新訂單 」 資料庫中的訂單。</span><span class="sxs-lookup"><span data-stu-id="6a10e-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="6a10e-108">使用動作 tooget 資料列、 插入新資料列，並且甚至刪除。</span><span class="sxs-lookup"><span data-stu-id="6a10e-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="6a10e-109">例如，在 Dynamics CRM Online 中建立記錄時 (觸發程序)，就會在 Oracle Database 中插入資料列 (動作)。</span><span class="sxs-lookup"><span data-stu-id="6a10e-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="6a10e-110">本主題說明如何 toouse hello 邏輯應用程式中的 Oracle 資料庫連接器。</span><span class="sxs-lookup"><span data-stu-id="6a10e-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a10e-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a10e-111">Prerequisites</span></span>

* <span data-ttu-id="6a10e-112">支援的 Oracle 版本：</span><span class="sxs-lookup"><span data-stu-id="6a10e-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="6a10e-113">Oracle 9 和更新版本</span><span class="sxs-lookup"><span data-stu-id="6a10e-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="6a10e-114">Oracle 用戶端軟體 8.1.7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="6a10e-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="6a10e-115">安裝 hello 在內部部署資料閘道。</span><span class="sxs-lookup"><span data-stu-id="6a10e-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="6a10e-116">[Tooon 內部部署資料連接的 logic apps 從](../logic-apps/logic-apps-gateway-connection.md)清單 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="6a10e-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="6a10e-117">在內部部署 Oracle 資料庫或以 Oracle DB 安裝 Azure VM 需要的 tooconnect tooan hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="6a10e-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="6a10e-118">hello 在內部部署資料閘道作為橋接器，並提供在內部部署資料 （不在 hello 雲端的資料） 與您的 logic apps 之間的安全資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="6a10e-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="6a10e-119">hello 相同閘道器可以使用多個服務，與多個資料來源。</span><span class="sxs-lookup"><span data-stu-id="6a10e-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="6a10e-120">因此，您可能只需要 tooinstall hello 閘道一次。</span><span class="sxs-lookup"><span data-stu-id="6a10e-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="6a10e-121">Hello hello 在內部部署資料閘道的安裝所在的電腦上安裝 Oracle 用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="6a10e-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="6a10e-122">請務必從 Oracle 的.NET tooinstall hello 64 位元 Oracle 資料提供者：</span><span class="sxs-lookup"><span data-stu-id="6a10e-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="6a10e-123">適用於 Windows x64 的 64 位元 ODAC 12c 版本 4 (12.1.0.2.4)</span><span class="sxs-lookup"><span data-stu-id="6a10e-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="6a10e-124">如果未安裝 hello Oracle 用戶端，嘗試 toocreate 或使用 hello 連線時，也會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6a10e-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="6a10e-125">請參閱本主題中的 hello 常見錯誤。</span><span class="sxs-lookup"><span data-stu-id="6a10e-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="6a10e-126">新增 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="6a10e-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a10e-127">此連接器並沒有任何觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6a10e-127">This connector does not have any triggers.</span></span> <span data-ttu-id="6a10e-128">只有動作。</span><span class="sxs-lookup"><span data-stu-id="6a10e-128">It has only actions.</span></span> <span data-ttu-id="6a10e-129">因此當您建立應用程式邏輯，加入另一個觸發程序 toostart 應用程式邏輯，例如**排程-循環**，或**要求 / 回應-回應**。</span><span class="sxs-lookup"><span data-stu-id="6a10e-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="6a10e-130">在 hello [Azure 入口網站](https://portal.azure.com)，建立空白的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a10e-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="6a10e-131">在 hello 啟動邏輯應用程式中，選取 hello**要求 / 回應-要求**觸發程序：</span><span class="sxs-lookup"><span data-stu-id="6a10e-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="6a10e-132">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="6a10e-132">Select **Save**.</span></span> <span data-ttu-id="6a10e-133">當您儲存時，系統會自動生產生一個要求 URL。</span><span class="sxs-lookup"><span data-stu-id="6a10e-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="6a10e-134">選取 [新增步驟]，再選取 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="6a10e-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="6a10e-135">在中輸入`oracle`toosee hello 可用的動作：</span><span class="sxs-lookup"><span data-stu-id="6a10e-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="6a10e-136">這也是最快方式 toosee hello hello 觸發程序和任何連接器可用動作。</span><span class="sxs-lookup"><span data-stu-id="6a10e-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="6a10e-137">輸入名稱的一部分 hello 連接器， `oracle`。</span><span class="sxs-lookup"><span data-stu-id="6a10e-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="6a10e-138">hello 設計工具會列出任何觸發程序和任何動作。</span><span class="sxs-lookup"><span data-stu-id="6a10e-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="6a10e-139">選取其中一個 hello 動作，例如**Oracle 資料庫-取得資料列**。</span><span class="sxs-lookup"><span data-stu-id="6a10e-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="6a10e-140">選取 [透過內部部署資料閘道連線]。</span><span class="sxs-lookup"><span data-stu-id="6a10e-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="6a10e-141">輸入 hello Oracle 伺服器名稱、 驗證方法、 使用者名稱、 密碼和選取 hello 閘道：</span><span class="sxs-lookup"><span data-stu-id="6a10e-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="6a10e-142">一旦連接之後，從 [hello] 清單中，選取資料表，然後輸入 hello 資料列識別碼 tooyour 資料表。</span><span class="sxs-lookup"><span data-stu-id="6a10e-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="6a10e-143">您需要 tooknow hello 識別碼 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="6a10e-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="6a10e-144">如果您不知道，請連絡您的 Oracle 資料庫管理員，並取得 hello 輸出`select * from yourTableName`。</span><span class="sxs-lookup"><span data-stu-id="6a10e-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="6a10e-145">這讓 hello 需要 tooproceed 的識別資訊。</span><span class="sxs-lookup"><span data-stu-id="6a10e-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="6a10e-146">在下列範例的 hello 中, 從人力資源資料庫傳回作業資料：</span><span class="sxs-lookup"><span data-stu-id="6a10e-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="6a10e-147">在下一個步驟中，您可以使用任何 hello 其他連接器 toobuild 您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="6a10e-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="6a10e-148">如果您想要從 Oracle、 tootest 取得資料，然後傳送給自己使用其中一種 hello hello Oracle 資料的電子郵件傳送電子郵件連接器，這類的 Office 365 或 Gmail。</span><span class="sxs-lookup"><span data-stu-id="6a10e-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="6a10e-149">使用來自 hello Oracle 資料表 toobuild hello hello 動態權杖`Subject`和`Body`的電子郵件：</span><span class="sxs-lookup"><span data-stu-id="6a10e-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="6a10e-150">**儲存**您的邏輯應用程式，接著選取 [執行]。</span><span class="sxs-lookup"><span data-stu-id="6a10e-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="6a10e-151">關閉 hello 設計工具，並查看 hello hello 狀態的執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="6a10e-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="6a10e-152">如果失敗，請選取 hello 失敗的訊息資料列。</span><span class="sxs-lookup"><span data-stu-id="6a10e-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="6a10e-153">hello designer 隨即開啟，並顯示您哪個步驟失敗，以及顯示 hello 資訊時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6a10e-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="6a10e-154">如果成功，您應該收到含有您所新增的 hello 資訊的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="6a10e-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="6a10e-155">工作流程想法</span><span class="sxs-lookup"><span data-stu-id="6a10e-155">Workflow ideas</span></span>

* <span data-ttu-id="6a10e-156">您想 toomonitor hello #oracle 雜湊標記，並放在資料庫中的 hello 推文，才能查詢，以及其他應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="6a10e-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="6a10e-157">在邏輯應用程式中，新增 hello`Twitter - When a new tweet is posted`觸發程序，然後輸入 hello **#oracle**雜湊標記。</span><span class="sxs-lookup"><span data-stu-id="6a10e-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="6a10e-158">接著，新增 hello`Oracle Database - Insert row`動作，然後選取您的資料表：</span><span class="sxs-lookup"><span data-stu-id="6a10e-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="6a10e-159">Tooa Service Bus 佇列時，會傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="6a10e-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="6a10e-160">您想 tooget 這些訊息，並將它們放在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="6a10e-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="6a10e-161">在邏輯應用程式中，新增 hello`Service Bus - when a message is received in a queue`觸發程序，並選取 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="6a10e-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="6a10e-162">接著，新增 hello`Oracle Database - Insert row`動作，然後選取您的資料表：</span><span class="sxs-lookup"><span data-stu-id="6a10e-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="6a10e-163">常見錯誤</span><span class="sxs-lookup"><span data-stu-id="6a10e-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="6a10e-164">**錯誤**： 無法連線到閘道 hello</span><span class="sxs-lookup"><span data-stu-id="6a10e-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="6a10e-165">**可能的原因**: hello 在內部部署資料閘道不能 tooconnect toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="6a10e-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="6a10e-166">**風險降低**： 請確定您的閘道器正在執行 hello 在內部部署電腦上，您已安裝，它可以連接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="6a10e-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="6a10e-167">我們建議不要安裝 hello 閘道可能已關閉的電腦或睡眠狀態。</span><span class="sxs-lookup"><span data-stu-id="6a10e-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="6a10e-168">您也可以重新啟動 hello 在內部部署資料閘道器服務 (2147463168 PBIEgwService)。</span><span class="sxs-lookup"><span data-stu-id="6a10e-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="6a10e-169">**錯誤**: hello 所使用的提供者已過時: ' system.data.oracleclient 需有 Oracle 用戶端軟體 8.1.7 或更新版本。 '。</span><span class="sxs-lookup"><span data-stu-id="6a10e-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="6a10e-170">請瀏覽[https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello 官方提供者。</span><span class="sxs-lookup"><span data-stu-id="6a10e-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="6a10e-171">**可能的原因**: hello Oracle 用戶端在 hello，hello 電腦未安裝 SDK 在內部部署資料閘道正在執行。</span><span class="sxs-lookup"><span data-stu-id="6a10e-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="6a10e-172">**解析**： 上下載並安裝 Oracle 用戶端 hello SDK hello 與 hello 在內部部署資料閘道相同的電腦。</span><span class="sxs-lookup"><span data-stu-id="6a10e-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="6a10e-173">**錯誤**：資料表 '[Tablename]' 並未定義任何索引鍵資料行</span><span class="sxs-lookup"><span data-stu-id="6a10e-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="6a10e-174">**可能的原因**: hello 資料表沒有任何主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="6a10e-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="6a10e-175">**解析**: hello Oracle 資料庫連接器需要有用於具有主索引鍵資料行的資料表。</span><span class="sxs-lookup"><span data-stu-id="6a10e-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="6a10e-176">目前不支援</span><span class="sxs-lookup"><span data-stu-id="6a10e-176">Currently not supported</span></span>

* <span data-ttu-id="6a10e-177">檢視和已存程序</span><span class="sxs-lookup"><span data-stu-id="6a10e-177">Views and stored procedures</span></span> 
* <span data-ttu-id="6a10e-178">包含複合索引鍵的任何資料表</span><span class="sxs-lookup"><span data-stu-id="6a10e-178">Any table with composite keys</span></span>
* <span data-ttu-id="6a10e-179">資料表中的巢狀物件類型</span><span class="sxs-lookup"><span data-stu-id="6a10e-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="6a10e-180">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="6a10e-180">Connector-specific details</span></span>

<span data-ttu-id="6a10e-181">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/oracle/)。</span><span class="sxs-lookup"><span data-stu-id="6a10e-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="6a10e-182">取得協助</span><span class="sxs-lookup"><span data-stu-id="6a10e-182">Get some help</span></span>

<span data-ttu-id="6a10e-183">hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)優越放置 tooask 問題、 回答的問題，以及查看其他邏輯應用程式使用者所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="6a10e-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="6a10e-184">您可以投票並在 [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish) 中提交意見，協助改善 Logic Apps 和連接器。</span><span class="sxs-lookup"><span data-stu-id="6a10e-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="6a10e-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a10e-185">Next steps</span></span>
<span data-ttu-id="6a10e-186">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)，並瀏覽 hello 在邏輯應用程式中可用的連接器我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="6a10e-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
