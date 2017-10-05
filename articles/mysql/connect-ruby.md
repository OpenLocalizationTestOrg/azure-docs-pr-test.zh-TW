---
title: "使用 Ruby 連線到 Azure Database for MySQL | Microsoft Docs"
description: "本快速入門提供數個 Ruby 程式碼範例，供您用來從 Azure Database for MySQL 連線及查詢資料。"
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
ms.openlocfilehash: e54f1dccbae060c52f48bfeb277c045b99a91715
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="972b5-103">Azure Database for MySQL︰使用 Ruby 來連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="972b5-103">Azure Database for MySQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="972b5-104">本快速入門示範如何從 Windows、Ubuntu Linux 和 Mac 平台使用 [Ruby](https://www.ruby-lang.org) 應用程式和 [mysql2](https://rubygems.org/gems/mysql2) Gem，連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="972b5-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and the [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="972b5-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="972b5-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="972b5-106">本文假設您已熟悉使用 Ruby 進行開發，但不熟悉 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="972b5-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="972b5-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="972b5-107">Prerequisites</span></span>
<span data-ttu-id="972b5-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="972b5-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="972b5-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="972b5-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="972b5-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="972b5-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="972b5-111">安裝 Ruby</span><span class="sxs-lookup"><span data-stu-id="972b5-111">Install Ruby</span></span>
<span data-ttu-id="972b5-112">在自己的電腦上安裝 Ruby、Gem 和 MySQL2 程式庫。</span><span class="sxs-lookup"><span data-stu-id="972b5-112">Install Ruby, Gem, and the MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="972b5-113">Windows</span><span class="sxs-lookup"><span data-stu-id="972b5-113">Windows</span></span>
1. <span data-ttu-id="972b5-114">下載並安裝 2.3 版的 [Ruby](http://rubyinstaller.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="972b5-114">Download and Install the 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="972b5-115">從 [開始] 功能表啟動新的命令提示 (cmd)。</span><span class="sxs-lookup"><span data-stu-id="972b5-115">Launch a new command prompt (cmd) from the Start menu.</span></span>
3. <span data-ttu-id="972b5-116">將目錄變更為 2.3 版的 Ruby 目錄。</span><span class="sxs-lookup"><span data-stu-id="972b5-116">Change directory into the Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="972b5-117">執行 `ruby -v` 命令以測試 Ruby 安裝，進而查看所安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="972b5-117">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
5. <span data-ttu-id="972b5-118">執行 `gem -v` 命令以測試 Gem 安裝，進而查看所安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="972b5-118">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
6. <span data-ttu-id="972b5-119">執行 `gem install mysql2` 命令以使用 Gem 建置適用於 Ruby 的 Mysql2 模組。</span><span class="sxs-lookup"><span data-stu-id="972b5-119">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="972b5-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="972b5-120">MacOS</span></span>
1. <span data-ttu-id="972b5-121">執行 `brew install ruby` 命令以使用 Homebrew 安裝 Ruby。</span><span class="sxs-lookup"><span data-stu-id="972b5-121">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="972b5-122">如需其他安裝選項，請參閱 Ruby [安裝文件](https://www.ruby-lang.org/en/documentation/installation/#homebrew)。</span><span class="sxs-lookup"><span data-stu-id="972b5-122">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="972b5-123">執行 `ruby -v` 命令以測試 Ruby 安裝，進而查看所安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="972b5-123">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="972b5-124">執行 `gem -v` 命令以測試 Gem 安裝，進而查看所安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="972b5-124">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
4. <span data-ttu-id="972b5-125">執行 `gem install mysql2` 命令以使用 Gem 建置適用於 Ruby 的 Mysql2 模組。</span><span class="sxs-lookup"><span data-stu-id="972b5-125">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="972b5-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="972b5-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="972b5-127">執行 `sudo apt-get install ruby-full` 命令來安裝 Ruby。</span><span class="sxs-lookup"><span data-stu-id="972b5-127">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="972b5-128">如需其他安裝選項，請參閱 Ruby [安裝文件](https://www.ruby-lang.org/en/documentation/installation/)。</span><span class="sxs-lookup"><span data-stu-id="972b5-128">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="972b5-129">執行 `ruby -v` 命令以測試 Ruby 安裝，進而查看所安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="972b5-129">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="972b5-130">執行 `sudo gem update --system` 命令以安裝 Gem 的最新更新。</span><span class="sxs-lookup"><span data-stu-id="972b5-130">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="972b5-131">執行 `gem -v` 命令以測試 Gem 安裝，進而查看所安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="972b5-131">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
5. <span data-ttu-id="972b5-132">執行 `sudo apt-get install build-essential` 命令以安裝 gcc、make 和其他建置工具。</span><span class="sxs-lookup"><span data-stu-id="972b5-132">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="972b5-133">執行 `sudo apt-get install libmysqlclient-dev` 命令以安裝 MySQL 用戶端開發人員程式庫。</span><span class="sxs-lookup"><span data-stu-id="972b5-133">Install the MySQL client developer libraries by running the command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="972b5-134">執行 `sudo gem install mysql2` 命令以使用 Gem 建置適用於 Ruby 的 mysql2 模組。</span><span class="sxs-lookup"><span data-stu-id="972b5-134">Build the mysql2 module for Ruby using Gem by running the command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="972b5-135">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="972b5-135">Get connection information</span></span>
<span data-ttu-id="972b5-136">取得連線到 Azure Database for MySQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="972b5-136">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="972b5-137">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="972b5-137">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="972b5-138">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="972b5-138">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="972b5-139">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您所建立的伺服器，例如 **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="972b5-139">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="972b5-140">按一下伺服器名稱 **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="972b5-140">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="972b5-141">選取伺服器的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="972b5-141">Select the server's **Properties** page.</span></span> <span data-ttu-id="972b5-142">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="972b5-142">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="972b5-143">![Azure Database for MySQL - 伺服器管理員登入](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="972b5-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="972b5-144">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="972b5-144">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="972b5-145">執行 Ruby 程式碼</span><span class="sxs-lookup"><span data-stu-id="972b5-145">Run Ruby code</span></span> 
1. <span data-ttu-id="972b5-146">將 Ruby 程式碼從下列區段貼到文字檔中，並將檔案儲存到專案資料夾中 (副檔名為 .rb)，例如 `C:\rubymysql\createtable.rb` 或 `/home/username/rubymysql/createtable.rb`。</span><span class="sxs-lookup"><span data-stu-id="972b5-146">Paste the Ruby code from the sections below into text files, and save the files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="972b5-147">若要執行程式碼，請啟動命令提示字元或 bash shell。</span><span class="sxs-lookup"><span data-stu-id="972b5-147">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="972b5-148">將目錄切換到專案資料夾 `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="972b5-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="972b5-149">然後，輸入後接檔案名稱的 ruby 命令 (例如 `ruby createtable.rb`) 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="972b5-149">Then type the ruby command followed by the file name, such as `ruby createtable.rb` to run the application.</span></span>
4. <span data-ttu-id="972b5-150">在 Windows 作業系統上，如果 ruby 應用程式不在您的 path 環境變數中，則可能需要使用完整路徑來啟動節點應用程式，例如 `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="972b5-150">On the Windows OS, if the ruby application is not in your path environment variable, you may need to use the full path to launch the node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="972b5-151">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="972b5-151">Connect and create a table</span></span>
<span data-ttu-id="972b5-152">使用下列程式碼搭配 **CREATE TABLE** SQL 陳述式 (後面接著 **INSERT INTO** SQL 陳述式) 來連線和建立資料表，進而將資料列新增至資料表中。</span><span class="sxs-lookup"><span data-stu-id="972b5-152">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="972b5-153">程式碼會使用 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) 類別 .new() 來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="972b5-153">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="972b5-154">然後它會呼叫 [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 方法數次來執行 DROP、CREATE TABLE 和 INSERT INTO 命令。</span><span class="sxs-lookup"><span data-stu-id="972b5-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="972b5-155">然後它會呼叫 [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 方法，在終止前關閉連線。</span><span class="sxs-lookup"><span data-stu-id="972b5-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="972b5-156">以您自己的值取代 `host`、`database`、`username` 和 `password` 字串。</span><span class="sxs-lookup"><span data-stu-id="972b5-156">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection to database.'

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

## <a name="read-data"></a><span data-ttu-id="972b5-157">讀取資料</span><span class="sxs-lookup"><span data-stu-id="972b5-157">Read data</span></span>
<span data-ttu-id="972b5-158">使用下列程式碼搭配 **SELECT** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="972b5-158">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="972b5-159">程式碼會使用 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) 類別 .new() 來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="972b5-159">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="972b5-160">然後它會呼叫 [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 方法來執行 SELECT 命令。</span><span class="sxs-lookup"><span data-stu-id="972b5-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the SELECT commands.</span></span> <span data-ttu-id="972b5-161">然後它會呼叫 [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 方法，在終止前關閉連線。</span><span class="sxs-lookup"><span data-stu-id="972b5-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="972b5-162">以您自己的值取代 `host`、`database`、`username` 和 `password` 字串。</span><span class="sxs-lookup"><span data-stu-id="972b5-162">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="update-data"></a><span data-ttu-id="972b5-163">更新資料</span><span class="sxs-lookup"><span data-stu-id="972b5-163">Update data</span></span>
<span data-ttu-id="972b5-164">使用下列程式碼搭配 **UPDATE** SQL 陳述式來連線和更新資料。</span><span class="sxs-lookup"><span data-stu-id="972b5-164">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="972b5-165">程式碼會使用 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) 類別 .new() 來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="972b5-165">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="972b5-166">然後它會呼叫 [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 方法來執行 UPDATE 命令。</span><span class="sxs-lookup"><span data-stu-id="972b5-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the UPDATE commands.</span></span> <span data-ttu-id="972b5-167">然後它會呼叫 [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 方法，在終止前關閉連線。</span><span class="sxs-lookup"><span data-stu-id="972b5-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="972b5-168">以您自己的值取代 `host`、`database`、`username` 和 `password` 字串。</span><span class="sxs-lookup"><span data-stu-id="972b5-168">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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


## <a name="delete-data"></a><span data-ttu-id="972b5-169">刪除資料</span><span class="sxs-lookup"><span data-stu-id="972b5-169">Delete data</span></span>
<span data-ttu-id="972b5-170">使用下列程式碼搭配 **DELETE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="972b5-170">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="972b5-171">程式碼會使用 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) 類別 .new() 來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="972b5-171">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="972b5-172">然後它會呼叫 [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 方法來執行 DELETE 命令。</span><span class="sxs-lookup"><span data-stu-id="972b5-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the DELETE commands.</span></span> <span data-ttu-id="972b5-173">然後它會呼叫 [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 方法，在終止前關閉連線。</span><span class="sxs-lookup"><span data-stu-id="972b5-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="972b5-174">以您自己的值取代 `host`、`database`、`username` 和 `password` 字串。</span><span class="sxs-lookup"><span data-stu-id="972b5-174">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="next-steps"></a><span data-ttu-id="972b5-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="972b5-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="972b5-176">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="972b5-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
