---
title: "aaaUse Azure 函式 tooperform 資料庫清除工作 |Microsoft 文件"
description: "使用 Azure 函式 tooschedule 連接 tooAzure SQL Database tooperiodically 工作清除的資料列。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="67378-103">使用 Azure 函式 tooconnect tooan Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="67378-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="67378-104">本主題說明您如何 toouse Azure 函式 toocreate 排程的作業清除 Azure SQL Database 中的資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="67378-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="67378-105">hello 新 C# 的函式會根據 hello Azure 入口網站中的預先定義的計時器觸發程序範本所建立。</span><span class="sxs-lookup"><span data-stu-id="67378-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="67378-106">toosupport 此案例中，您也必須設定資料庫連接字串為 hello 函式應用程式中的設定。</span><span class="sxs-lookup"><span data-stu-id="67378-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="67378-107">此案例使用大量作業對 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="67378-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="67378-108">toohave 您函式處理個別 CRUD 作業行動應用程式資料表中的，您應該改為使用[行動應用程式繫結](functions-bindings-mobile-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="67378-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67378-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="67378-109">Prerequisites</span></span>

+ <span data-ttu-id="67378-110">本主題使用計時器觸發的函數。</span><span class="sxs-lookup"><span data-stu-id="67378-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="67378-111">Hello 主題中的步驟完成 hello[計時器所觸發的 Azure 中建立的函式](functions-create-scheduled-function.md)toocreate C# 版本，此函式。</span><span class="sxs-lookup"><span data-stu-id="67378-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="67378-112">本主題示範 hello 中執行大量的清除作業的 TRANSACT-SQL 命令**SalesOrderHeader** hello 有提供 AdventureWorksLT 範例資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="67378-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="67378-113">hello 主題中步驟的 toocreate hello 有提供 AdventureWorksLT 範例資料庫，完整 hello [hello Azure 入口網站中建立 Azure SQL database](../sql-database/sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="67378-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="67378-114">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="67378-114">Get connection information</span></span>

<span data-ttu-id="67378-115">當您完成時，您所建立的 hello 資料庫所需 tooget hello 連接字串[hello Azure 入口網站中建立 Azure SQL database](../sql-database/sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="67378-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="67378-116">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="67378-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="67378-117">選取**SQL 資料庫**從 hello 左側功能表中，選取您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="67378-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="67378-118">選取**顯示資料庫的連接字串**及完成複製 hello **ADO.NET**連接字串。</span><span class="sxs-lookup"><span data-stu-id="67378-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![複製 hello ADO.NET 連接字串。](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="67378-120">設定 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="67378-120">Set hello connection string</span></span> 

<span data-ttu-id="67378-121">函式應用程式裝載函式在 Azure 中的 hello 執行。</span><span class="sxs-lookup"><span data-stu-id="67378-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="67378-122">它是最佳的作法 toostore 連接字串和函式應用程式設定中的其他密碼。</span><span class="sxs-lookup"><span data-stu-id="67378-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="67378-123">使用應用程式設定可避免無意間洩露的 hello 與您的程式碼的連接字串。</span><span class="sxs-lookup"><span data-stu-id="67378-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="67378-124">瀏覽您所建立的 tooyour 函式應用程式[計時器所觸發的 Azure 中建立的函式](functions-create-scheduled-function.md)。</span><span class="sxs-lookup"><span data-stu-id="67378-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="67378-125">選取 [平台功能] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="67378-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Hello 函式應用程式的應用程式設定。](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="67378-127">向下捲動太**連接字串**並加入使用 hello 設定 hello 資料表中所指定的連接字串。</span><span class="sxs-lookup"><span data-stu-id="67378-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![加入連接字串 toohello 函式應用程式設定。](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="67378-129">設定</span><span class="sxs-lookup"><span data-stu-id="67378-129">Setting</span></span>       | <span data-ttu-id="67378-130">建議的值</span><span class="sxs-lookup"><span data-stu-id="67378-130">Suggested value</span></span> | <span data-ttu-id="67378-131">說明</span><span class="sxs-lookup"><span data-stu-id="67378-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="67378-132">**名稱**</span><span class="sxs-lookup"><span data-stu-id="67378-132">**Name**</span></span>  |  <span data-ttu-id="67378-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="67378-133">sqldb_connection</span></span>  | <span data-ttu-id="67378-134">使用的 tooaccess hello 函式程式碼中儲存連接字串。</span><span class="sxs-lookup"><span data-stu-id="67378-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="67378-135">**值**</span><span class="sxs-lookup"><span data-stu-id="67378-135">**Value**</span></span> | <span data-ttu-id="67378-136">複製的字串</span><span class="sxs-lookup"><span data-stu-id="67378-136">Copied string</span></span>  | <span data-ttu-id="67378-137">過去的 hello 連接字串中複製 hello 上一節。</span><span class="sxs-lookup"><span data-stu-id="67378-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="67378-138">**類型**</span><span class="sxs-lookup"><span data-stu-id="67378-138">**Type**</span></span> | <span data-ttu-id="67378-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="67378-139">SQL Database</span></span> | <span data-ttu-id="67378-140">使用 hello 預設 SQL 資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="67378-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="67378-141">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="67378-141">Click **Save**.</span></span>

<span data-ttu-id="67378-142">現在，您可以加入 hello C# 函式程式碼連接 tooyour SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="67378-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="67378-143">更新函數程式碼</span><span class="sxs-lookup"><span data-stu-id="67378-143">Update your function code</span></span>

1. <span data-ttu-id="67378-144">在應用程式的函式，選取 hello 計時器觸發函式。</span><span class="sxs-lookup"><span data-stu-id="67378-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="67378-145">新增下列頂端 hello hello 現有函式程式碼的組件參考的 hello:</span><span class="sxs-lookup"><span data-stu-id="67378-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="67378-146">新增下列 hello`using`陳述式 toohello 函式：</span><span class="sxs-lookup"><span data-stu-id="67378-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="67378-147">取代現有的 hello**執行**以下列程式碼的 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="67378-147">Replace hello existing **Run** function with hello following code:</span></span>
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="67378-148">此範例命令會更新 hello**狀態**hello 出貨日期為基礎的資料行。</span><span class="sxs-lookup"><span data-stu-id="67378-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="67378-149">其應該會更新 32 個資料列。</span><span class="sxs-lookup"><span data-stu-id="67378-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="67378-150">按一下**儲存**，監看式 hello**記錄**windows hello 接下來函式執行，則請注意 hello hello 中更新資料列數目**SalesOrderHeader**資料表。</span><span class="sxs-lookup"><span data-stu-id="67378-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![檢視 hello 函式記錄檔。](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="67378-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67378-152">Next steps</span></span>

<span data-ttu-id="67378-153">接下來，深入了解如何 toouse 函式與 Logic Apps toointegrate 與其他服務。</span><span class="sxs-lookup"><span data-stu-id="67378-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="67378-154">建立與 Logic Apps 整合的函數</span><span class="sxs-lookup"><span data-stu-id="67378-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="67378-155">如需函式的詳細資訊，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="67378-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="67378-156">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="67378-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="67378-157">可供程式設計人員撰寫函數程式碼及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="67378-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="67378-158">測試 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="67378-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="67378-159">說明可用於測試函式的各種工具和技巧。</span><span class="sxs-lookup"><span data-stu-id="67378-159">Describes various tools and techniques for testing your functions.</span></span>  
