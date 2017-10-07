---
title: "Azure SQL Database 的拼音 tooquery aaaUse |Microsoft 文件"
description: "本主題說明如何 toouse 拼音 toocreate 連接 tooan Azure SQL Database 和查詢使用 TRANSACT-SQL 陳述式的程式。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>使用拼音 tooquery Azure SQL database

本快速入門教學課程示範如何 toouse [Ruby](https://www.ruby-lang.org) toocreate 程式 tooconnect tooan Azure SQL 資料庫，將 TRANSACT-SQL 陳述式 tooquery 資料。

## <a name="prerequisites"></a>必要條件

toocomplete 此快速入門教學課程，請確定您擁有 hello 下列必要條件：

- Azure SQL Database。 本快速入門會使用 hello 資源建立在其中一個這些快速入門： 

   - [建立 DB - 入口網站](sql-database-get-started-portal.md)
   - [建立 DB - CLI](sql-database-get-started-cli.md)
   - [建立 DB - PowerShell](sql-database-get-started-powershell.md)

- A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。
- 您已安裝適用於您作業系統的 Ruby 和相關軟體。
    - **MacOS**：安裝 Homebrew、安裝 rbenv 和 ruby-build、安裝 Ruby，然後安裝 FreeTDS。 請參閱[步驟 1.2、1.3、1.4 和 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/)。
    - **Ubuntu**：安裝 Ruby 的必要條件、安裝 rbenv 和 ruby-build、安裝 Ruby，然後安裝 FreeTDS。 請參閱[步驟 1.2、1.3、1.4 和 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/)。

## <a name="sql-server-connection-information"></a>SQL Server 連線資訊

收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。 您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 
3. 在 hello**概觀**為您的資料庫頁面上，檢閱 hello 完整的伺服器名稱。 您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項，hello 下列影像所示：

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. 如果您的 Azure SQL Database 伺服器忘記 hello 登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。

> [!IMPORTANT]
> 防火牆規則必須可供您執行本教學課程中的 hello 電腦的 hello 公用 IP 位址。 如果您在不同電腦上或有不同的公用 IP 位址，建立[伺服器層級防火牆規則使用 hello Azure 入口網站](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。 

## <a name="insert-code-tooquery-sql-database"></a>插入程式碼 tooquery SQL 資料庫

1. 在您慣用的文字編輯器中，建立新的檔案 **sqltest.rb**

2. 以下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼的 hello 取代 hello 內容。

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a>執行 hello 程式碼

1. 在 hello 命令提示字元中執行下列命令的 hello:

   ```bash
   ruby sqltest.rb
   ```

2. 請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。


## <a name="next-steps"></a>後續步驟
- [設計您的第一個 Azure SQL Database](sql-database-design-first-database.md)
- [適用於 TinyTDS 的 GitHub 存放庫](https://github.com/rails-sqlserver/tiny_tds)
- [回報或發問有關 TinyTDS 的問題](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Ruby Drivers for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
