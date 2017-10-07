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
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>使用 Azure 函式 tooconnect tooan Azure SQL Database
本主題說明您如何 toouse Azure 函式 toocreate 排程的作業清除 Azure SQL Database 中的資料表中的資料列。 hello 新 C# 的函式會根據 hello Azure 入口網站中的預先定義的計時器觸發程序範本所建立。 toosupport 此案例中，您也必須設定資料庫連接字串為 hello 函式應用程式中的設定。 此案例使用大量作業對 hello 資料庫。 toohave 您函式處理個別 CRUD 作業行動應用程式資料表中的，您應該改為使用[行動應用程式繫結](functions-bindings-mobile-apps.md)。

## <a name="prerequisites"></a>必要條件

+ 本主題使用計時器觸發的函數。 Hello 主題中的步驟完成 hello[計時器所觸發的 Azure 中建立的函式](functions-create-scheduled-function.md)toocreate C# 版本，此函式。   

+ 本主題示範 hello 中執行大量的清除作業的 TRANSACT-SQL 命令**SalesOrderHeader** hello 有提供 AdventureWorksLT 範例資料庫中的資料表。 hello 主題中步驟的 toocreate hello 有提供 AdventureWorksLT 範例資料庫，完整 hello [hello Azure 入口網站中建立 Azure SQL database](../sql-database/sql-database-get-started-portal.md)。 

## <a name="get-connection-information"></a>取得連線資訊

當您完成時，您所建立的 hello 資料庫所需 tooget hello 連接字串[hello Azure 入口網站中建立 Azure SQL database](../sql-database/sql-database-get-started-portal.md)。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
 
3. 選取**SQL 資料庫**從 hello 左側功能表中，選取您的資料庫上 hello **SQL 資料庫**頁面。

4. 選取**顯示資料庫的連接字串**及完成複製 hello **ADO.NET**連接字串。

    ![複製 hello ADO.NET 連接字串。](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>設定 hello 連接字串 

函式應用程式裝載函式在 Azure 中的 hello 執行。 它是最佳的作法 toostore 連接字串和函式應用程式設定中的其他密碼。 使用應用程式設定可避免無意間洩露的 hello 與您的程式碼的連接字串。 

1. 瀏覽您所建立的 tooyour 函式應用程式[計時器所觸發的 Azure 中建立的函式](functions-create-scheduled-function.md)。

2. 選取 [平台功能] > [應用程式設定]。
   
    ![Hello 函式應用程式的應用程式設定。](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. 向下捲動太**連接字串**並加入使用 hello 設定 hello 資料表中所指定的連接字串。
   
    ![加入連接字串 toohello 函式應用程式設定。](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | 設定       | 建議的值 | 說明             | 
    | ------------ | ------------------ | --------------------- | 
    | **名稱**  |  sqldb_connection  | 使用的 tooaccess hello 函式程式碼中儲存連接字串。    |
    | **值** | 複製的字串  | 過去的 hello 連接字串中複製 hello 上一節。 |
    | **類型** | SQL Database | 使用 hello 預設 SQL 資料庫連接。 |   

3. 按一下 [儲存] 。

現在，您可以加入 hello C# 函式程式碼連接 tooyour SQL 資料庫。

## <a name="update-your-function-code"></a>更新函數程式碼

1. 在應用程式的函式，選取 hello 計時器觸發函式。
 
3. 新增下列頂端 hello hello 現有函式程式碼的組件參考的 hello:

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. 新增下列 hello`using`陳述式 toohello 函式：
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. 取代現有的 hello**執行**以下列程式碼的 hello 函式：
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

    此範例命令會更新 hello**狀態**hello 出貨日期為基礎的資料行。 其應該會更新 32 個資料列。

5. 按一下**儲存**，監看式 hello**記錄**windows hello 接下來函式執行，則請注意 hello hello 中更新資料列數目**SalesOrderHeader**資料表。

    ![檢視 hello 函式記錄檔。](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>後續步驟

接下來，深入了解如何 toouse 函式與 Logic Apps toointegrate 與其他服務。

> [!div class="nextstepaction"] 
> [建立與 Logic Apps 整合的函數](functions-twitter-email.md)

如需函式的詳細資訊，請參閱下列主題中的 hello:

* [Azure Functions 開發人員參考](functions-reference.md)  
  可供程式設計人員撰寫函數程式碼及定義觸發程序和繫結時參考。
* [測試 Azure Functions](functions-test-a-function.md)  
  說明可用於測試函式的各種工具和技巧。  
