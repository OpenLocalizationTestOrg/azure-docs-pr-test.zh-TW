---
title: "VS Code：在 Azure SQL Database 中連接和查詢資料 | Microsoft Docs"
description: "深入了解如何 tooconnect tooSQL 資料庫在 Azure 上使用 Visual Studio 程式碼。 然後，執行 TRANSACT-SQL (T-SQL) 陳述式 tooquery 和編輯資料。"
metacanonical: 
keywords: "連接 toosql 資料庫"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a>Azure SQL Database： 使用 Visual Studio 程式碼 tooconnect 和查詢資料

[Visual Studio Code](https://code.visualstudio.com/docs)是適用於 Linux，macOS，圖形化的程式碼編輯器，可支援擴充功能，包括 Windows hello [mssql 延伸](https://aka.ms/mssql-marketplace)Microsoft SQL Server、 Azure SQL Database 和 SQL 資料倉儲查詢。 本快速入門示範如何 toouse Visual Studio Code tooconnect tooan Azure SQL database，然後再使用 TRANSACT-SQL 陳述式 tooquery，插入、 更新和刪除 hello 資料庫中的資料。

## <a name="prerequisites"></a>必要條件

本快速入門會使用為其起始點 hello 的資源建立在其中一個這些快速入門：

- [建立 DB - 入口網站](sql-database-get-started-portal.md)
- [建立 DB - CLI](sql-database-get-started-cli.md)
- [建立 DB - PowerShell](sql-database-get-started-powershell.md)

開始之前，請確定您已安裝最新版本的中 hello [Visual Studio 程式碼](https://code.visualstudio.com/Download)並載入的 hello [mssql 延伸](https://aka.ms/mssql-marketplace)。 如需安裝 hello mssql 擴充功能的指引，請參閱[安裝 VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) ，請參閱[mssql Visual Studio 程式碼](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)。 

## <a name="configure-vs-code"></a>設定 VS Code 

### <a name="mac-os"></a>**Mac OS**
MacOS，您需要 tooinstall 也就是先決條件的 DotNet 核心該 mssql 附檔名不會使用 OpenSSL。 開啟您的終端機，並輸入下列命令 tooinstall hello **brew**和**OpenSSL**。 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**

不需要特別設定。

### <a name="windows"></a>**Windows**

不需要特別設定。

## <a name="sql-server-connection-information"></a>SQL Server 連線資訊

收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。 您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 
3. 在 hello**概觀**頁面為您的資料庫檢閱 hello 完整伺服器名稱 hello 下列影像所示。 您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。

   ![連線資訊](./media/sql-database-connect-query-dotnet/server-name.png) 

4. 如果您的 Azure SQL Database 伺服器忘記 hello 登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。 

## <a name="set-language-mode-toosql"></a>設定語言模式 tooSQL

設定 hello 語言模式設定得**SQL** Visual Studio Code tooenable mssql 命令以及 T-SQL IntelliSense。

1. 開啟新的 Visual Studio Code 視窗。 

2. 按一下**純文字**hello 右下角的 hello 狀態列中。
3. 在 hello**選取的語言模式**開啟下拉式選單中，輸入**SQL**，然後按**ENTER** tooset hello 語言模式 tooSQL。 

   ![SQL 語言模式](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a>連接 tooyour 資料庫

使用 Visual Studio Code tooestablish 連接 tooyour Azure SQL Database 伺服器。

> [!IMPORTANT]
> 在繼續之前，確定您已備妥伺服器、資料庫和登入資訊。 您開始輸入 hello 連線設定檔資訊，如果您將焦點變更 Visual Studio 程式碼，您便可以 toorestart 建立 hello 連線設定檔。
>

1. 在 VS Code 按**CTRL + SHIFT + P** (或**F1**) tooopen hello 命令選擇區。

2. 輸入 **sqlcon** 並且按 **ENTER**。

3. 按**ENTER** tooselect**建立連線設定檔**。 這會為您的 SQL Server 執行個體建立連線設定檔。

4. 請遵循 hello 提示 toospecify hello 連接 hello 新連線設定檔的內容。 指定每個值之後, 按**ENTER** toocontinue。 

   | 設定       | 建議的值 | 說明 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱 | hello 完整的伺服器名稱 | hello 名稱應該像下面這樣： **mynewserver20170313.database.windows.net**。 |
   | **資料庫名稱** | mySampleDatabase | hello 資料庫 toowhich tooconnect hello 名稱。 |
   | **驗證** | SQL 登入| SQL 驗證是我們已在此教學課程中的 hello 唯一的驗證類型。 |
   | **使用者名稱** | hello 伺服器系統管理員帳戶 | 這是您指定當您建立 hello 伺服器 hello 帳戶。 |
   | **密碼 (SQL 登入)** | hello 伺服器系統管理員帳戶的密碼 | 這是您指定當您建立 hello 伺服器 hello 密碼。 |
   | **儲存密碼？** | 是或否 | 如果您不想 tooenter hello 密碼每次，請選取 [是]。 |
   | **輸入這個設定檔的名稱** | 設定檔名稱，例如 **mySampleDatabase** | 儲存設定檔名稱可讓您在後續登入時加快連線速度。 | 

5. 按 hello **ESC**金鑰 tooclose hello 資訊訊息，通知您已建立 hello 設定檔，並連接。

6. 請確認您 hello 狀態列中的連線。

   ![連線狀態](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>查詢資料

使用 hello 下列程式碼 tooquery 的 hello 前 20 個產品類別目錄使用 hello[選取](https://msdn.microsoft.com/library/ms189499.aspx)TRANSACT-SQL 陳述式。

1. 在 hello**編輯器**視窗中，輸入下列查詢在 hello 空白查詢視窗中的 hello:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. 按**CTRL + SHIFT + E** tooretrieve hello Product 和 ProductCategory 資料表的資料。

    ![查詢](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>插入資料

使用 hello 下列程式碼會 tooinsert 新產品到 hello SalesLT.Product 資料表使用 hello[插入](https://msdn.microsoft.com/library/ms174335.aspx)TRANSACT-SQL 陳述式。

1. 在 hello**編輯器**視窗中，刪除 hello 上一個查詢，然後輸入 hello 下列查詢：

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. 按**CTRL + SHIFT + E** tooinsert hello Product 資料表中的新資料列。

## <a name="update-data"></a>更新資料

使用 hello 下列程式碼 tooupdate hello 新產品您先前加入使用 hello[更新](https://msdn.microsoft.com/library/ms177523.aspx)TRANSACT-SQL 陳述式。

1.  在 hello**編輯器**視窗中，刪除 hello 上一個查詢，然後輸入 hello 下列查詢：

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. 按**CTRL + SHIFT + E** tooupdate hello 指定的資料列 hello Product 資料表中。

## <a name="delete-data"></a>刪除資料

使用 hello 下列程式碼 toodelete hello 新產品您先前加入使用 hello[刪除](https://msdn.microsoft.com/library/ms189835.aspx)TRANSACT-SQL 陳述式。

1. 在 hello**編輯器**視窗中，刪除 hello 上一個查詢，然後輸入 hello 下列查詢：

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. 按**CTRL + SHIFT + E** toodelete hello 指定的資料列 hello Product 資料表中。

## <a name="next-steps"></a>後續步驟

- tooconnect 和查詢中使用 SQL Server Management Studio，請參閱[連接和查詢使用 SSMS](sql-database-connect-query-ssms.md)。
- 如需有關使用 Visual Studio Code 的 MSDN 雜誌文章，請參閱[使用 MSSQL 擴充功能建立資料庫 IDE 部落格文章](https://msdn.microsoft.com/magazine/mt809115)。
