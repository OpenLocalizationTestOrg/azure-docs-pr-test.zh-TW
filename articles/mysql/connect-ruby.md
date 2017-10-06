---
title: "用於使用 Ruby MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門會提供數個拼音的程式碼範例，您可以使用 tooconnect 和查詢資料從 Azure 資料庫的 MySQL。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>Azure 資料庫的 MySQL： 使用 Ruby tooconnect 和查詢資料
本快速入門示範如何使用 MySQL 資料庫的 tooconnect tooan Azure [Ruby](https://www.ruby-lang.org)應用程式和 hello [mysql2](https://rubygems.org/gems/mysql2)健身從 Windows、 Ubuntu Linux 和 Mac 平台。 它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。 本文假設您熟悉開發使用 Ruby，但是，您就可以與 MySQL 的 Azure 資料庫的新 tooworking。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a>安裝 Ruby
在自己電腦上安裝 Ruby、 健身和 hello MySQL2 程式庫。 

### <a name="windows"></a>Windows
1. 下載並安裝 hello 2.3 版本[Ruby](http://rubyinstaller.org/downloads/)。
2. 從 hello [開始] 功能表中啟動新的命令提示字元 (cmd)。
3. 將目錄變更到 hello 版本 2.3 的拼音目錄。 `cd c:\Ruby23-x64\bin`
4. 測試 hello 拼音安裝執行 hello 命令`ruby -v`toosee hello 版本安裝。
5. 藉由執行 hello 命令測試 hello 健身安裝`gem -v`toosee hello 版本安裝。
6. 建置執行 hello 命令使用寶石的 Ruby hello Mysql2 模組`gem install mysql2`。

### <a name="macos"></a>MacOS
1. 安裝執行 hello 命令使用 Homebrew Ruby `brew install ruby`。 如需其他安裝選項，請參閱 hello Ruby[安裝文件集](https://www.ruby-lang.org/en/documentation/installation/#homebrew)。
2. 測試 hello 拼音安裝執行 hello 命令`ruby -v`toosee hello 版本安裝。
3. 藉由執行 hello 命令測試 hello 健身安裝`gem -v`toosee hello 版本安裝。
4. 建置執行 hello 命令使用寶石的 Ruby hello Mysql2 模組`gem install mysql2`。

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. 執行 hello 命令來安裝 Ruby `sudo apt-get install ruby-full`。 如需其他安裝選項，請參閱 hello Ruby[安裝文件集](https://www.ruby-lang.org/en/documentation/installation/)。
2. 測試 hello 拼音安裝執行 hello 命令`ruby -v`toosee hello 版本安裝。
3. 安裝執行 hello 命令 hello 最新更新健身`sudo gem update --system`。
4. 藉由執行 hello 命令測試 hello 健身安裝`gem -v`toosee hello 版本安裝。
5. 執行 hello 命令來安裝 hello gcc、 樣式及其他建置工具`sudo apt-get install build-essential`。
6. 執行 hello 命令來安裝 MySQL 用戶端開發人員程式庫 hello `sudo apt-get install libmysqlclient-dev`。
7. 建置執行 hello 命令使用寶石的 Ruby hello mysql2 模組`sudo gem install mysql2`。

## <a name="get-connection-information"></a>取得連線資訊
取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您有 creased，例如 hello 伺服器**myserver4demo**。
3. 按一下伺服器名稱，hello **myserver4demo**。
4. 選取 hello 伺服器**屬性**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for MySQL - 伺服器管理員登入](./media/connect-ruby/1_server-properties-name-login.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。

## <a name="run-ruby-code"></a>執行 Ruby 程式碼 
1. Hello hello 各節中的拼音程式碼貼入文字檔案，然後 hello 檔案儲存到專案資料夾與檔案延伸模組需要.rb，例如`C:\rubymysql\createtable.rb`或`/home/username/rubymysql/createtable.rb`。
2. toorun hello 程式碼中，啟動 hello 命令提示字元，或被殼層。 將目錄切換到專案資料夾 `cd rubymysql`
3. 然後輸入 hello 拼音命令後面 hello 檔案名稱，例如`ruby createtable.rb`toorun hello 應用程式。
4. 在 hello Windows 作業系統，如果 hello ruby 應用程式不在 path 環境變數，您可能需要 toouse hello 完整路徑 toolaunch hello node 應用程式例如`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>連線及建立資料表
使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式，後面接著**INSERT INTO** hello 資料表的 SQL 陳述式 tooadd 資料列。

hello 程式碼會使用[mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8)類別 MySQL.new() 方法 tooconnect tooAzure 資料庫。 然後它會呼叫方法[query （)](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage)多次 toorun hello 卸除、 CREATE TABLE 和 INSERT INTO 命令。 然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello 連線後，再終止。

取代 hello `host`， `database`， `username`，和`password`字串以您自己的值。 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a>讀取資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。 

hello 程式碼會使用[mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8)類別 MySQL.new() 方法 tooconnect tooAzure 資料庫。 然後它會呼叫方法[query （)](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello 選取命令。 然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello 連線後，再終止。

取代 hello `host`， `database`， `username`，和`password`字串以您自己的值。 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。

hello 程式碼會使用[mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8)類別 MySQL.new() 方法 tooconnect tooAzure 資料庫。 然後它會呼叫方法[query （)](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello 更新命令。 然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello 連線後，再終止。

取代 hello `host`， `database`， `username`，和`password`字串以您自己的值。 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。 

hello 程式碼會使用[mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8)類別 MySQL.new() 方法 tooconnect tooAzure 資料庫。 然後它會呼叫方法[query （)](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE 命令。 然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello 連線後，再終止。

取代 hello `host`， `database`， `username`，和`password`字串以您自己的值。 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [使用匯出和匯入來移轉資料庫](./concepts-migrate-import-export.md)
