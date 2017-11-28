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
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="c38ac-103">Azure 資料庫的 MySQL： 使用 Ruby tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="c38ac-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="c38ac-104">本快速入門示範如何使用 MySQL 資料庫的 tooconnect tooan Azure [Ruby](https://www.ruby-lang.org)應用程式和 hello [mysql2](https://rubygems.org/gems/mysql2)健身從 Windows、 Ubuntu Linux 和 Mac 平台。</span><span class="sxs-lookup"><span data-stu-id="c38ac-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="c38ac-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="c38ac-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="c38ac-106">本文假設您熟悉開發使用 Ruby，但是，您就可以與 MySQL 的 Azure 資料庫的新 tooworking。</span><span class="sxs-lookup"><span data-stu-id="c38ac-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c38ac-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="c38ac-107">Prerequisites</span></span>
<span data-ttu-id="c38ac-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="c38ac-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="c38ac-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="c38ac-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="c38ac-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="c38ac-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="c38ac-111">安裝 Ruby</span><span class="sxs-lookup"><span data-stu-id="c38ac-111">Install Ruby</span></span>
<span data-ttu-id="c38ac-112">在自己電腦上安裝 Ruby、 健身和 hello MySQL2 程式庫。</span><span class="sxs-lookup"><span data-stu-id="c38ac-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="c38ac-113">Windows</span><span class="sxs-lookup"><span data-stu-id="c38ac-113">Windows</span></span>
1. <span data-ttu-id="c38ac-114">下載並安裝 hello 2.3 版本[Ruby](http://rubyinstaller.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="c38ac-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="c38ac-115">從 hello [開始] 功能表中啟動新的命令提示字元 (cmd)。</span><span class="sxs-lookup"><span data-stu-id="c38ac-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="c38ac-116">將目錄變更到 hello 版本 2.3 的拼音目錄。</span><span class="sxs-lookup"><span data-stu-id="c38ac-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="c38ac-117">測試 hello 拼音安裝執行 hello 命令`ruby -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="c38ac-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="c38ac-118">藉由執行 hello 命令測試 hello 健身安裝`gem -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="c38ac-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="c38ac-119">建置執行 hello 命令使用寶石的 Ruby hello Mysql2 模組`gem install mysql2`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="c38ac-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="c38ac-120">MacOS</span></span>
1. <span data-ttu-id="c38ac-121">安裝執行 hello 命令使用 Homebrew Ruby `brew install ruby`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="c38ac-122">如需其他安裝選項，請參閱 hello Ruby[安裝文件集](https://www.ruby-lang.org/en/documentation/installation/#homebrew)。</span><span class="sxs-lookup"><span data-stu-id="c38ac-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="c38ac-123">測試 hello 拼音安裝執行 hello 命令`ruby -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="c38ac-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="c38ac-124">藉由執行 hello 命令測試 hello 健身安裝`gem -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="c38ac-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="c38ac-125">建置執行 hello 命令使用寶石的 Ruby hello Mysql2 模組`gem install mysql2`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="c38ac-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="c38ac-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="c38ac-127">執行 hello 命令來安裝 Ruby `sudo apt-get install ruby-full`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="c38ac-128">如需其他安裝選項，請參閱 hello Ruby[安裝文件集](https://www.ruby-lang.org/en/documentation/installation/)。</span><span class="sxs-lookup"><span data-stu-id="c38ac-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="c38ac-129">測試 hello 拼音安裝執行 hello 命令`ruby -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="c38ac-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="c38ac-130">安裝執行 hello 命令 hello 最新更新健身`sudo gem update --system`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="c38ac-131">藉由執行 hello 命令測試 hello 健身安裝`gem -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="c38ac-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="c38ac-132">執行 hello 命令來安裝 hello gcc、 樣式及其他建置工具`sudo apt-get install build-essential`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="c38ac-133">執行 hello 命令來安裝 MySQL 用戶端開發人員程式庫 hello `sudo apt-get install libmysqlclient-dev`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="c38ac-134">建置執行 hello 命令使用寶石的 Ruby hello mysql2 模組`sudo gem install mysql2`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c38ac-135">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="c38ac-135">Get connection information</span></span>
<span data-ttu-id="c38ac-136">取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c38ac-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="c38ac-137">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="c38ac-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="c38ac-138">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="c38ac-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c38ac-139">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您有 creased，例如 hello 伺服器**myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="c38ac-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="c38ac-140">按一下伺服器名稱，hello **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="c38ac-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="c38ac-141">選取 hello 伺服器**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="c38ac-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="c38ac-142">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="c38ac-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="c38ac-143">![Azure Database for MySQL - 伺服器管理員登入](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="c38ac-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="c38ac-144">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="c38ac-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="c38ac-145">執行 Ruby 程式碼</span><span class="sxs-lookup"><span data-stu-id="c38ac-145">Run Ruby code</span></span> 
1. <span data-ttu-id="c38ac-146">Hello hello 各節中的拼音程式碼貼入文字檔案，然後 hello 檔案儲存到專案資料夾與檔案延伸模組需要.rb，例如`C:\rubymysql\createtable.rb`或`/home/username/rubymysql/createtable.rb`。</span><span class="sxs-lookup"><span data-stu-id="c38ac-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="c38ac-147">toorun hello 程式碼中，啟動 hello 命令提示字元，或被殼層。</span><span class="sxs-lookup"><span data-stu-id="c38ac-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="c38ac-148">將目錄切換到專案資料夾 `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="c38ac-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="c38ac-149">然後輸入 hello 拼音命令後面 hello 檔案名稱，例如`ruby createtable.rb`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c38ac-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="c38ac-150">在 hello Windows 作業系統，如果 hello ruby 應用程式不在 path 環境變數，您可能需要 toouse hello 完整路徑 toolaunch hello node 應用程式例如`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="c38ac-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="c38ac-151">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="c38ac-151">Connect and create a table</span></span>
<span data-ttu-id="c38ac-152">使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式，後面接著**INSERT INTO** hello 資料表的 SQL 陳述式 tooadd 資料列。</span><span class="sxs-lookup"><span data-stu-id="c38ac-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="c38ac-153">hello 程式碼會使用[mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8)類別 MySQL.new() 方法 tooconnect tooAzure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c38ac-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="c38ac-154">然後它會呼叫方法[query （)](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage)多次 toorun hello 卸除、 CREATE TABLE 和 INSERT INTO 命令。</span><span class="sxs-lookup"><span data-stu-id="c38ac-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="c38ac-155">然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello 連線後，再終止。</span><span class="sxs-lookup"><span data-stu-id="c38ac-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="c38ac-156">取代 hello `host`， `database`， `username`，和`password`字串以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="c38ac-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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

## <a name="read-data"></a><span data-ttu-id="c38ac-157">讀取資料</span><span class="sxs-lookup"><span data-stu-id="c38ac-157">Read data</span></span>
<span data-ttu-id="c38ac-158">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c38ac-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="c38ac-159">hello 程式碼會使用[mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8)類別 MySQL.new() 方法 tooconnect tooAzure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c38ac-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="c38ac-160">然後它會呼叫方法[query （)](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello 選取命令。</span><span class="sxs-lookup"><span data-stu-id="c38ac-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="c38ac-161">然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello 連線後，再終止。</span><span class="sxs-lookup"><span data-stu-id="c38ac-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="c38ac-162">取代 hello `host`， `database`， `username`，和`password`字串以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="c38ac-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="c38ac-163">更新資料</span><span class="sxs-lookup"><span data-stu-id="c38ac-163">Update data</span></span>
<span data-ttu-id="c38ac-164">使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c38ac-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="c38ac-165">hello 程式碼會使用[mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8)類別 MySQL.new() 方法 tooconnect tooAzure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c38ac-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="c38ac-166">然後它會呼叫方法[query （)](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello 更新命令。</span><span class="sxs-lookup"><span data-stu-id="c38ac-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="c38ac-167">然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello 連線後，再終止。</span><span class="sxs-lookup"><span data-stu-id="c38ac-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="c38ac-168">取代 hello `host`， `database`， `username`，和`password`字串以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="c38ac-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="c38ac-169">刪除資料</span><span class="sxs-lookup"><span data-stu-id="c38ac-169">Delete data</span></span>
<span data-ttu-id="c38ac-170">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c38ac-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="c38ac-171">hello 程式碼會使用[mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8)類別 MySQL.new() 方法 tooconnect tooAzure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c38ac-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="c38ac-172">然後它會呼叫方法[query （)](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE 命令。</span><span class="sxs-lookup"><span data-stu-id="c38ac-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="c38ac-173">然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello 連線後，再終止。</span><span class="sxs-lookup"><span data-stu-id="c38ac-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="c38ac-174">取代 hello `host`， `database`， `username`，和`password`字串以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="c38ac-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="c38ac-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c38ac-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c38ac-176">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="c38ac-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
