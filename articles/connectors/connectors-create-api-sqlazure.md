---
title: "在您的 Logic Apps aaaAdd hello Azure SQL Database 連接器 |Microsoft 文件"
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
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="d0ac6-103">開始使用 hello Azure SQL Database 連接器</span><span class="sxs-lookup"><span data-stu-id="d0ac6-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="d0ac6-104">使用 hello Azure SQL Database 連接器，建立為您的組織管理資料在資料表中的工作流程。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="d0ac6-105">利用 SQL Database，您可以：</span><span class="sxs-lookup"><span data-stu-id="d0ac6-105">With SQL Database, you:</span></span>

* <span data-ttu-id="d0ac6-106">建置您的工作流程加入新的客戶 tooa 客戶資料庫，或更新訂單 」 資料庫中的訂單。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="d0ac6-107">使用動作 tooget 資料列、 插入新資料列，並且甚至刪除。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="d0ac6-108">例如，當有記錄在 Dynamics CRM Online 中建立時 (觸發程序)，則在 Azure SQL Database 插入資料列 (動作)。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="d0ac6-109">本主題說明您如何 toouse hello 邏輯應用程式中的 SQL Database 連接器及清單也 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="d0ac6-110">toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="d0ac6-111">連接 tooAzure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d0ac6-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="d0ac6-112">邏輯應用程式可以存取任何服務之前，您先建立*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="d0ac6-113">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="d0ac6-114">例如，tooconnect tooSQL 資料庫，您先建立 SQL Database*連接*。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="d0ac6-115">toocreate 連線，您輸入您平常用 tooaccess hello 服務，您所連接的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="d0ac6-116">因此，在 SQL 資料庫中，輸入您 SQL 資料庫認證 toocreate hello 連接。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="d0ac6-117">建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="d0ac6-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="d0ac6-118">使用觸發程序</span><span class="sxs-lookup"><span data-stu-id="d0ac6-118">Use a trigger</span></span>
<span data-ttu-id="d0ac6-119">此連接器並沒有任何觸發程序。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-119">This connector does not have any triggers.</span></span> <span data-ttu-id="d0ac6-120">使用其他觸發程序 toostart hello 邏輯應用程式，例如循環觸發程序、 HTTP Webhook 觸發程序、 觸發程序適用於其他連接器，等等。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="d0ac6-121">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md) 可提供範例。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="d0ac6-122">使用動作</span><span class="sxs-lookup"><span data-stu-id="d0ac6-122">Use an action</span></span>
<span data-ttu-id="d0ac6-123">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="d0ac6-124">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="d0ac6-125">選取加號 hello。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-125">Select hello plus sign.</span></span> <span data-ttu-id="d0ac6-126">您會看到幾個選擇：**將動作加入**，**加入條件**，或其中一個 hello**詳細**選項。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="d0ac6-127">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="d0ac6-128">在 [hello] 文字方塊中，輸入"sql"tooget 所有 hello 可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="d0ac6-129">在我們的範例中，選擇 [SQL Server - 取得資料列]。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="d0ac6-130">如果連接已存在，然後選取 hello**資料表名稱**從 hello 下拉式清單，然後輸入 hello**資料列識別碼**想 tooreturn。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="d0ac6-131">如果系統提示您輸入 hello 連接資訊，然後輸入 hello 詳細資料 toocreate hello 連接。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="d0ac6-132">[建立 hello 連接](connectors-create-api-sqlazure.md#create-the-connection)本主題說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d0ac6-133">在此範例中，我們會從資料表傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="d0ac6-134">在這個資料列，toosee hello 資料加入另一個使用 hello 資料表中的 hello 欄位建立檔的動作。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="d0ac6-135">比方說，將會使用 hello FirstName 和 LastName 欄位 toocreate hello 雲端儲存體帳戶中的新檔案的 OneDrive 動作。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="d0ac6-136">**儲存**您的變更 （hello 工具列的左上的角）。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="d0ac6-137">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="d0ac6-138">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="d0ac6-138">Connector-specific details</span></span>

<span data-ttu-id="d0ac6-139">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/sql/)。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d0ac6-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0ac6-140">Next steps</span></span>
<span data-ttu-id="d0ac6-141">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="d0ac6-142">瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="d0ac6-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

