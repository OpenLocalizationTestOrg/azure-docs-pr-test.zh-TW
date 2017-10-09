---
title: "Azure SQL Database 的 aaaUse Python tooquery |Microsoft 文件"
description: "本主題說明如何 toouse Python toocreate 連接 tooan Azure SQL Database 和查詢使用 TRANSACT-SQL 陳述式的程式。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a>使用 Python tooquery Azure SQL database

 本快速入門示範如何 toouse [Python](https://python.org) tooconnect tooan Azure SQL 資料庫，將 TRANSACT-SQL 陳述式 tooquery 資料。

## <a name="prerequisites"></a>必要條件

toocomplete 此快速入門教學課程，請確定您擁有 hello 下列：

- Azure SQL Database。 本快速入門會使用 hello 資源建立在其中一個這些快速入門： 

   - [建立 DB - 入口網站](sql-database-get-started-portal.md)
   - [建立 DB - CLI](sql-database-get-started-cli.md)
   - [建立 DB - PowerShell](sql-database-get-started-powershell.md)

- A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。

- 您已安裝適用於您作業系統的 Python 和相關軟體。

    - **MacOS**： 安裝 Homebrew，並將 Python，安裝 hello ODBC 驅動程式和 SQLCMD，，然後再安裝 SQL server 的 hello Python 驅動程式。 請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/)。
    - **Ubuntu**： 安裝 Python 和其他封裝，然後再安裝 hello Python 驅動程式 SQL Server 所需。 請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/)。
    - **Windows**: hello 的 Python （您現在已設定環境變數） 的最新版本的安裝，安裝 hello ODBC 驅動程式和 SQLCMD，然後再安裝 hello Python 驅動程式適用於 SQL Server。 請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/)。 

## <a name="sql-server-connection-information"></a>SQL Server 連線資訊

收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。 您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 
3. 在 hello**概觀**頁面為您的資料庫檢閱 hello 完整伺服器名稱 hello 下列影像所示。 您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. 如果忘記您的伺服器登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。     
    
## <a name="insert-code-tooquery-sql-database"></a>插入程式碼 tooquery SQL 資料庫 

1. 在您慣用的文字編輯器中，建立新的檔案 **sqltest.py**。  

2. 以下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼的 hello 取代 hello 內容。

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a>執行 hello 程式碼

1. 在 hello 命令提示字元中執行下列命令的 hello:

   ```Python
   python sqltest.py
   ```

2. 請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。

## <a name="next-steps"></a>後續步驟

- [設計您的第一個 Azure SQL Database](sql-database-design-first-database.md)
- [Microsoft Python Drivers for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [Python 開發人員中心](https://azure.microsoft.com/develop/python/?v=17.23h)

