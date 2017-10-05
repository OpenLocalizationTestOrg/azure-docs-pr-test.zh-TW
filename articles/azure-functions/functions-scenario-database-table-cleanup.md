---
title: "使用 Azure Functions 執行資料庫清除工作 | Microsoft Docs"
description: "使用 Azure Functions 排程可連接到 Azure SQL Database 以定期清除資料列的工作。"
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
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="738e2-103">使用 Azure Functions 連接到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="738e2-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="738e2-104">本主題示範如何使用 Azure Functions 建立可清除 Azure SQL Database 資料表中資料列的排程作業。</span><span class="sxs-lookup"><span data-stu-id="738e2-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="738e2-105">新的 C# 函數是根據 Azure 入口網站中預先定義的計時器觸發程序範本所建立。</span><span class="sxs-lookup"><span data-stu-id="738e2-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="738e2-106">若要支援此案例，您也必須在函數應用程式中設定資料庫連接字串作為設定。</span><span class="sxs-lookup"><span data-stu-id="738e2-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="738e2-107">此案例會對資料庫使用大量作業。</span><span class="sxs-lookup"><span data-stu-id="738e2-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="738e2-108">若要讓您的函數程序在 Mobile Apps 資料表中進行個別的 CRUD 作業，您應該改用 [Mobile Apps 繫結](functions-bindings-mobile-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="738e2-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="738e2-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="738e2-109">Prerequisites</span></span>

+ <span data-ttu-id="738e2-110">本主題使用計時器觸發的函數。</span><span class="sxs-lookup"><span data-stu-id="738e2-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="738e2-111">完成主題[在 Azure 中建立由計時器觸發的函數](functions-create-scheduled-function.md)中的步驟，以建立此函數的 C# 版本。</span><span class="sxs-lookup"><span data-stu-id="738e2-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="738e2-112">本主題將示範在 AdventureWorksLT 範例資料庫的 **SalesOrderHeader** 資料表中執行大量清除作業的 Transact-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="738e2-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="738e2-113">若要建立 AdventureWorksLT 範例資料庫，請完成本主題[在 Azure 入口網站中建立 Azure SQL 資料庫](../sql-database/sql-database-get-started-portal.md)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="738e2-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="738e2-114">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="738e2-114">Get connection information</span></span>

<span data-ttu-id="738e2-115">完成[在 Azure 入口網站中建立 Azure SQL 資料庫](../sql-database/sql-database-get-started-portal.md)時，您必須取得所建立之資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="738e2-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="738e2-116">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="738e2-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="738e2-117">從左側功能表中選取 [SQL Database]，然後選取 [SQL 資料庫] 頁面上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="738e2-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="738e2-118">選取 [顯示資料庫連接字串]，然後複製完整的 **ADO.NET** 連接字串。</span><span class="sxs-lookup"><span data-stu-id="738e2-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![複製 ADO.NET 連接字串。](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="738e2-120">設定連接字串</span><span class="sxs-lookup"><span data-stu-id="738e2-120">Set the connection string</span></span> 

<span data-ttu-id="738e2-121">函式應用程式可在 Azure 中主控函式的執行。</span><span class="sxs-lookup"><span data-stu-id="738e2-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="738e2-122">在函數應用程式設定中儲存連接字串和其他機密資料是最佳做法。</span><span class="sxs-lookup"><span data-stu-id="738e2-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="738e2-123">使用應用程式設定可避免意外洩露連接字串與您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="738e2-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="738e2-124">瀏覽至您建立的函數應用程式。[在 Azure 中建立由計時器觸發的函數](functions-create-scheduled-function.md)。</span><span class="sxs-lookup"><span data-stu-id="738e2-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="738e2-125">選取 [平台功能] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="738e2-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![函數應用程式的應用程式設定。](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="738e2-127">向下捲動至 [連接字串]，然後使用資料表中指定的設定來新增連接字串。</span><span class="sxs-lookup"><span data-stu-id="738e2-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![將連接字串新增至函數應用程式設定。](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="738e2-129">設定</span><span class="sxs-lookup"><span data-stu-id="738e2-129">Setting</span></span>       | <span data-ttu-id="738e2-130">建議的值</span><span class="sxs-lookup"><span data-stu-id="738e2-130">Suggested value</span></span> | <span data-ttu-id="738e2-131">說明</span><span class="sxs-lookup"><span data-stu-id="738e2-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="738e2-132">**名稱**</span><span class="sxs-lookup"><span data-stu-id="738e2-132">**Name**</span></span>  |  <span data-ttu-id="738e2-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="738e2-133">sqldb_connection</span></span>  | <span data-ttu-id="738e2-134">用於存取函數程式碼的預存連接字串。</span><span class="sxs-lookup"><span data-stu-id="738e2-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="738e2-135">**值**</span><span class="sxs-lookup"><span data-stu-id="738e2-135">**Value**</span></span> | <span data-ttu-id="738e2-136">複製的字串</span><span class="sxs-lookup"><span data-stu-id="738e2-136">Copied string</span></span>  | <span data-ttu-id="738e2-137">貼上您在上一節中複製的連接字串。</span><span class="sxs-lookup"><span data-stu-id="738e2-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="738e2-138">**類型**</span><span class="sxs-lookup"><span data-stu-id="738e2-138">**Type**</span></span> | <span data-ttu-id="738e2-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="738e2-139">SQL Database</span></span> | <span data-ttu-id="738e2-140">使用預設的 SQL Database 連接。</span><span class="sxs-lookup"><span data-stu-id="738e2-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="738e2-141">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="738e2-141">Click **Save**.</span></span>

<span data-ttu-id="738e2-142">現在，您可以加入 C# 函數程式碼來連接到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="738e2-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="738e2-143">更新函數程式碼</span><span class="sxs-lookup"><span data-stu-id="738e2-143">Update your function code</span></span>

1. <span data-ttu-id="738e2-144">在函數應用程式中，選取計時器觸發的函數。</span><span class="sxs-lookup"><span data-stu-id="738e2-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="738e2-145">在現有函數程式碼頂端新增下列組件參考：</span><span class="sxs-lookup"><span data-stu-id="738e2-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="738e2-146">將下列 `using` 陳述式加入至函數：</span><span class="sxs-lookup"><span data-stu-id="738e2-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="738e2-147">使用下列程式碼來取代現有的 **Run** 函數：</span><span class="sxs-lookup"><span data-stu-id="738e2-147">Replace the existing **Run** function with the following code:</span></span>
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
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="738e2-148">此範例命令會根據出貨日期來更新 **Status** 資料行。</span><span class="sxs-lookup"><span data-stu-id="738e2-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="738e2-149">其應該會更新 32 個資料列。</span><span class="sxs-lookup"><span data-stu-id="738e2-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="738e2-150">按一下 [儲存]、針對下一個函數執行監看 [記錄] 視窗，然後記下 **SalesOrderHeader** 資料表中更新的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="738e2-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![檢視函數記錄。](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="738e2-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="738e2-152">Next steps</span></span>

<span data-ttu-id="738e2-153">接下來，了解如何將 Functions 與 Logic Apps 搭配使用以與其他服務整合。</span><span class="sxs-lookup"><span data-stu-id="738e2-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="738e2-154">建立與 Logic Apps 整合的函數</span><span class="sxs-lookup"><span data-stu-id="738e2-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="738e2-155">如需有關 Functions 的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="738e2-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="738e2-156">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="738e2-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="738e2-157">可供程式設計人員撰寫函數程式碼及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="738e2-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="738e2-158">測試 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="738e2-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="738e2-159">說明可用於測試函式的各種工具和技巧。</span><span class="sxs-lookup"><span data-stu-id="738e2-159">Describes various tools and techniques for testing your functions.</span></span>  
