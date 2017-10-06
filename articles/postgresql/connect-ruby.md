---
title: "aaaConnect tooAzure 使用 Ruby PostgreSQL 資料庫 |Microsoft 文件"
description: "本快速入門提供拼音的程式碼範例，您可以使用 tooconnect 和 PostgreSQL 查詢從 Azure 資料庫的資料。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a>Azure PostgreSQL 資料庫： 使用 Ruby tooconnect 和查詢資料
本快速入門示範如何使用 PostgreSQL 資料庫的 tooconnect tooan Azure [Ruby](https://www.ruby-lang.org)應用程式。 它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。 本文假設您熟悉開發使用 Ruby，但是，您就可以新增 tooworking Azure PostgreSQL 資料庫。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [建立 DB - 入口網站](quickstart-create-server-database-portal.md)
- [建立 DB - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>安裝 Ruby
在自己的電腦上安裝 Ruby。 

### <a name="windows"></a>Windows
- 下載並安裝 hello 最新版本[Ruby](http://rubyinstaller.org/downloads/)。
- 在 hello 完成畫面 hello MSI 安裝程式，請檢查 hello 方塊，指出 「 執行 'ridk install' tooinstall MSYS2 和開發工具鏈。 」 然後按一下 **完成**toolaunch hello 下一個安裝程式。
- hello RubyInstaller2 適用於 Windows 的安裝程式會啟動。 輸入 2 tooinstall hello MSYS2 儲存機制更新。 它完成並傳回 toohello 安裝提示之後，關閉 hello 命令視窗。
- 從 hello [開始] 功能表中啟動新的命令提示字元 (cmd)。
- 測試 hello 拼音安裝`ruby -v`toosee hello 版本安裝。
- 測試 hello 健身安裝`gem -v`toosee hello 版本安裝。
- 建置執行 hello 命令使用寶石的 Ruby hello PostgreSQL 模組`gem install pg`。

### <a name="macos"></a>MacOS
- 安裝執行 hello 命令使用 Homebrew Ruby `brew install ruby`。 如需其他安裝選項，請參閱 hello Ruby[安裝文件集](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- 測試 hello 拼音安裝`ruby -v`toosee hello 版本安裝。
- 測試 hello 健身安裝`gem -v`toosee hello 版本安裝。
- 建置執行 hello 命令使用寶石的 Ruby hello PostgreSQL 模組`gem install pg`。

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- 執行 hello 命令來安裝 Ruby `sudo apt-get install ruby-full`。 如需其他安裝選項，請參閱 hello Ruby[安裝文件集](https://www.ruby-lang.org/en/documentation/installation/)。
- 測試 hello 拼音安裝`ruby -v`toosee hello 版本安裝。
- 安裝執行 hello 命令 hello 最新更新健身`sudo gem update --system`。
- 測試 hello 健身安裝`gem -v`toosee hello 版本安裝。
- 執行 hello 命令來安裝 hello gcc、 樣式及其他建置工具`sudo apt-get install build-essential`。
- 執行 hello 命令來安裝 hello PostgreSQL 程式庫`sudo apt-get install libpq-dev`。
- 建置執行 hello 命令使用健身 hello 拼音 pg 模組`sudo gem install pg`。

## <a name="run-ruby-code"></a>執行 Ruby 程式碼 
- Hello 程式碼儲存到文字檔，並儲存 hello 檔案到專案資料夾與檔案延伸模組需要.rb，例如`C:\rubypostgres\read.rb`或`/home/username/rubypostgres/read.rb`
- toorun hello 程式碼中，啟動 hello 命令提示字元，或被殼層。 將目錄切換到您的專案資料夾`cd rubypostgres`，然後輸入 hello 命令`ruby read.rb`toorun hello 應用程式。

## <a name="get-connection-information"></a>取得連線資訊
取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**mypgserver 20170401**。
3. 按一下伺服器名稱，hello **mypgserver 20170401**。
4. 選取 hello 伺服器**概觀**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-ruby/1-connection-string.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱。 如有需要，重設 hello 密碼。

## <a name="connect-and-create-a-table"></a>連線及建立資料表
使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式，後面接著**INSERT INTO** hello 資料表的 SQL 陳述式 tooadd 資料列。

hello 程式碼會使用[PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection)具有建構函式物件[new （)](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 資料庫。 然後它會呼叫方法[exec （)](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello 卸除、 CREATE TABLE 和 INSERT INTO 命令。 hello 程式碼會檢查是否有錯誤使用 hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error)類別。 然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello 連線後，再終止。

取代 hello `host`， `database`， `user`，和`password`字串以您自己的值。 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a>讀取資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。 

hello 程式碼會使用[PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection)具有建構函式物件[new （)](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 資料庫。 然後它會呼叫方法[exec （)](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT 命令，將 hello 結果保留在結果集。 hello 結果集的集合會一直重複使用 hello`resultSet.each do`迴圈，hello 目前資料列的值保持在 hello`row`變數。 hello 程式碼會檢查是否有錯誤使用 hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error)類別。 然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello 連線後，再終止。

取代 hello `host`， `database`， `user`，和`password`字串以您自己的值。 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。

hello 程式碼會使用[PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection)具有建構函式物件[new （)](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 資料庫。 然後它會呼叫方法[exec （)](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello 更新命令。 hello 程式碼會檢查是否有錯誤使用 hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error)類別。 然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello 連線後，再終止。

取代 hello `host`， `database`， `user`，和`password`字串以您自己的值。 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。 

hello 程式碼會使用[PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection)具有建構函式物件[new （)](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 資料庫。 然後它會呼叫方法[exec （)](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello 更新命令。 hello 程式碼會檢查是否有錯誤使用 hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error)類別。 然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello 連線後，再終止。

取代 hello `host`， `database`， `user`，和`password`字串以您自己的值。 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [使用匯出和匯入來移轉資料庫](./howto-migrate-using-export-and-import.md)
