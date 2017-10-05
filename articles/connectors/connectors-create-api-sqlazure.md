---
title: "在您的 Logic Apps 中新增 Azure SQL Database 連接器 | Microsoft Docs"
description: "搭配 REST API 參數來使用 Azure SQL Database 連接器的概觀"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="e7796-103">開始使用 Azure SQL Database 連接器</span><span class="sxs-lookup"><span data-stu-id="e7796-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="e7796-104">使用 Azure SQL Database 連接器，為組織建立工作流程來管理資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="e7796-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="e7796-105">利用 SQL Database，您可以：</span><span class="sxs-lookup"><span data-stu-id="e7796-105">With SQL Database, you:</span></span>

* <span data-ttu-id="e7796-106">藉由在客戶資料庫中新增新客戶或在訂單資料庫中更新訂單，以建置工作流程。</span><span class="sxs-lookup"><span data-stu-id="e7796-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="e7796-107">使用動作來取得一列資料、插入新的資料列，甚至加以刪除。</span><span class="sxs-lookup"><span data-stu-id="e7796-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="e7796-108">例如，當有記錄在 Dynamics CRM Online 中建立時 (觸發程序)，則在 Azure SQL Database 插入資料列 (動作)。</span><span class="sxs-lookup"><span data-stu-id="e7796-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="e7796-109">本主題說明如何在邏輯應用程式中使用 SQL Database 連接器，並且也列出動作。</span><span class="sxs-lookup"><span data-stu-id="e7796-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="e7796-110">若要深入瞭解 Logic Apps，請參閱[什麼是邏輯應用程式](../logic-apps/logic-apps-what-are-logic-apps.md)以及[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="e7796-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="e7796-111">連線到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e7796-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="e7796-112">您必須先建立與服務的「連線」，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="e7796-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="e7796-113">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="e7796-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="e7796-114">例如，若要連線到 SQL Database，您必須先建立 SQL Database「連線」。</span><span class="sxs-lookup"><span data-stu-id="e7796-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="e7796-115">若要建立連線，您需要輸入平常用來存取所連線服務的認證。</span><span class="sxs-lookup"><span data-stu-id="e7796-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="e7796-116">因此，在 SQL Database 中，請輸入 SQL Database 認證來建立連線。</span><span class="sxs-lookup"><span data-stu-id="e7796-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="e7796-117">建立連線</span><span class="sxs-lookup"><span data-stu-id="e7796-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="e7796-118">使用觸發程序</span><span class="sxs-lookup"><span data-stu-id="e7796-118">Use a trigger</span></span>
<span data-ttu-id="e7796-119">此連接器並沒有任何觸發程序。</span><span class="sxs-lookup"><span data-stu-id="e7796-119">This connector does not have any triggers.</span></span> <span data-ttu-id="e7796-120">請使用其他觸發程序來啟動邏輯應用程式，例如循環觸發程序、HTTP Webhook 觸發程序、其他連接器適用的觸發程序等等。</span><span class="sxs-lookup"><span data-stu-id="e7796-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="e7796-121">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md) 可提供範例。</span><span class="sxs-lookup"><span data-stu-id="e7796-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="e7796-122">使用動作</span><span class="sxs-lookup"><span data-stu-id="e7796-122">Use an action</span></span>
<span data-ttu-id="e7796-123">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="e7796-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="e7796-124">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="e7796-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e7796-125">選取加號。</span><span class="sxs-lookup"><span data-stu-id="e7796-125">Select the plus sign.</span></span> <span data-ttu-id="e7796-126">您會看到幾個選擇︰[新增動作]、[新增條件] 或其中一個 [其他] 選項。</span><span class="sxs-lookup"><span data-stu-id="e7796-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="e7796-127">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="e7796-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e7796-128">在文字方塊中，輸入「sql」以取得所有可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="e7796-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="e7796-129">在我們的範例中，選擇 [SQL Server - 取得資料列]。</span><span class="sxs-lookup"><span data-stu-id="e7796-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="e7796-130">如果連線已存在，則選取下拉式清單中的 [資料表名稱]，然後輸入想要傳回的 [資料列識別碼]。</span><span class="sxs-lookup"><span data-stu-id="e7796-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="e7796-131">如果系統提示您輸入連線資訊，請輸入詳細資料以建立連線。</span><span class="sxs-lookup"><span data-stu-id="e7796-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="e7796-132">本主題的[建立連線](connectors-create-api-sqlazure.md#create-the-connection)一節會說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="e7796-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e7796-133">在此範例中，我們會從資料表傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="e7796-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="e7796-134">若要查看此資料列中的資料，請新增另一個動作，以使用資料表中的欄位建立檔案。</span><span class="sxs-lookup"><span data-stu-id="e7796-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="e7796-135">例如，新增 OneDrive 動作，使用 [FirstName] 和 [LastName] 欄位在雲端儲存體帳戶中建立新檔案。</span><span class="sxs-lookup"><span data-stu-id="e7796-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="e7796-136">**儲存**您的變更 (工具列的左上角)。</span><span class="sxs-lookup"><span data-stu-id="e7796-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="e7796-137">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="e7796-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="e7796-138">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="e7796-138">Connector-specific details</span></span>

<span data-ttu-id="e7796-139">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/sql/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="e7796-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e7796-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7796-140">Next steps</span></span>
<span data-ttu-id="e7796-141">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="e7796-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e7796-142">請到我們的 [API 清單](apis-list.md)探索 Logic Apps 中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="e7796-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

