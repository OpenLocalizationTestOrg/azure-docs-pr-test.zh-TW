---
title: "使用 Ruby 連線至 Azure Database for PostgreSQL | Microsoft Docs"
description: "本快速入門提供 Ruby 程式碼範例，您可用於從 Azure Database for PostgreSQL 連線及查詢資料。"
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
ms.openlocfilehash: 9153a5a843dd5c18f27a3af232fea3b152240fe1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="c2112-103">Azure Database for PostgreSQL︰使用 Ruby 連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="c2112-103">Azure Database for PostgreSQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="c2112-104">本快速入門示範如何使用 [Ruby](https://www.ruby-lang.org) 應用程式來連線到 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="c2112-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="c2112-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="c2112-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="c2112-106">本文假設您已熟悉使用 Ruby 進行開發，但不熟悉 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="c2112-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2112-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="c2112-107">Prerequisites</span></span>
<span data-ttu-id="c2112-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="c2112-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="c2112-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="c2112-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="c2112-110">建立 DB - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c2112-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="c2112-111">安裝 Ruby</span><span class="sxs-lookup"><span data-stu-id="c2112-111">Install Ruby</span></span>
<span data-ttu-id="c2112-112">在自己的電腦上安裝 Ruby。</span><span class="sxs-lookup"><span data-stu-id="c2112-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="c2112-113">Windows</span><span class="sxs-lookup"><span data-stu-id="c2112-113">Windows</span></span>
- <span data-ttu-id="c2112-114">下載並安裝最新版的 [Ruby](http://rubyinstaller.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="c2112-114">Download and Install the latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="c2112-115">在 MSI 安裝程式的完成畫面上，核取表示「執行 'ridk install' 以安裝 MSYS2 和開發工具鏈」的方塊。</span><span class="sxs-lookup"><span data-stu-id="c2112-115">On the finish screen of the MSI installer, check the box that says "Run 'ridk install' to install MSYS2 and development toolchain."</span></span> <span data-ttu-id="c2112-116">然後按一下 [完成] 以啟動下一個安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c2112-116">Then click **Finish** to launch the next installer.</span></span>
- <span data-ttu-id="c2112-117">RubyInstaller2 for Windows 安裝程式隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="c2112-117">The RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="c2112-118">輸入 2 以安裝 MSYS2 存放庫更新。</span><span class="sxs-lookup"><span data-stu-id="c2112-118">Type 2 to install the MSYS2 repository update.</span></span> <span data-ttu-id="c2112-119">在完成並返回安裝提示之後，請關閉命令視窗。</span><span class="sxs-lookup"><span data-stu-id="c2112-119">After it finishes and returns to the installation prompt, close the command window.</span></span>
- <span data-ttu-id="c2112-120">從 [開始] 功能表啟動新的命令提示 (cmd)。</span><span class="sxs-lookup"><span data-stu-id="c2112-120">Launch a new command prompt (cmd) from the Start menu.</span></span>
- <span data-ttu-id="c2112-121">測試 Ruby 安裝 `ruby -v` 以查看安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c2112-121">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="c2112-122">測試 Gem 安裝 `gem -v` 以查看安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c2112-122">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="c2112-123">執行 `gem install pg` 命令以使用 Gem 建置 PostgreSQL 模組。</span><span class="sxs-lookup"><span data-stu-id="c2112-123">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="c2112-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="c2112-124">MacOS</span></span>
- <span data-ttu-id="c2112-125">執行 `brew install ruby` 命令以使用 Homebrew 安裝 Ruby。</span><span class="sxs-lookup"><span data-stu-id="c2112-125">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="c2112-126">如需其他安裝選項，請參閱 Ruby [安裝文件](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="c2112-126">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="c2112-127">測試 Ruby 安裝 `ruby -v` 以查看安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c2112-127">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="c2112-128">測試 Gem 安裝 `gem -v` 以查看安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c2112-128">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="c2112-129">執行 `gem install pg` 命令以使用 Gem 建置 PostgreSQL 模組。</span><span class="sxs-lookup"><span data-stu-id="c2112-129">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="c2112-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="c2112-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="c2112-131">執行 `sudo apt-get install ruby-full` 命令來安裝 Ruby。</span><span class="sxs-lookup"><span data-stu-id="c2112-131">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="c2112-132">如需其他安裝選項，請參閱 Ruby [安裝文件](https://www.ruby-lang.org/en/documentation/installation/)。</span><span class="sxs-lookup"><span data-stu-id="c2112-132">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="c2112-133">測試 Ruby 安裝 `ruby -v` 以查看安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c2112-133">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="c2112-134">執行 `sudo gem update --system` 命令以安裝 Gem 的最新更新。</span><span class="sxs-lookup"><span data-stu-id="c2112-134">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
- <span data-ttu-id="c2112-135">測試 Gem 安裝 `gem -v` 以查看安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c2112-135">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="c2112-136">執行 `sudo apt-get install build-essential` 命令以安裝 gcc、make 和其他建置工具。</span><span class="sxs-lookup"><span data-stu-id="c2112-136">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="c2112-137">執行 `sudo apt-get install libpq-dev` 命令以安裝 PostgreSQL 程式庫。</span><span class="sxs-lookup"><span data-stu-id="c2112-137">Install the PostgreSQL libraries by running the command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="c2112-138">執行 `sudo gem install pg` 命令以使用 Gem 建置 Ruby pg 模組。</span><span class="sxs-lookup"><span data-stu-id="c2112-138">Build the Ruby pg module using Gem by running the command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="c2112-139">執行 Ruby 程式碼</span><span class="sxs-lookup"><span data-stu-id="c2112-139">Run Ruby code</span></span> 
- <span data-ttu-id="c2112-140">將程式碼儲存到專案資料夾中副檔名為 .rb 的文字檔中，例如 `C:\rubypostgres\read.rb` 或 `/home/username/rubypostgres/read.rb`。</span><span class="sxs-lookup"><span data-stu-id="c2112-140">Save the code into a text file, and save the file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="c2112-141">若要執行程式碼，請啟動命令提示字元或 bash shell。</span><span class="sxs-lookup"><span data-stu-id="c2112-141">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="c2112-142">將目錄變更為您的專案資料夾 `cd rubypostgres`，然後輸入 `ruby read.rb` 命令來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2112-142">Change directory into your project folder `cd rubypostgres`, then type the command `ruby read.rb` to run the application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c2112-143">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="c2112-143">Get connection information</span></span>
<span data-ttu-id="c2112-144">取得連線到 Azure Database for PostgreSQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="c2112-144">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="c2112-145">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="c2112-145">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="c2112-146">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="c2112-146">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c2112-147">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您所建立的伺服器，例如 **mypgserver-20170401**。</span><span class="sxs-lookup"><span data-stu-id="c2112-147">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="c2112-148">按一下伺服器名稱 [mypgserver-20170401]。</span><span class="sxs-lookup"><span data-stu-id="c2112-148">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="c2112-149">選取伺服器的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="c2112-149">Select the server's **Overview** page.</span></span> <span data-ttu-id="c2112-150">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="c2112-150">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="c2112-151">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="c2112-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="c2112-152">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="c2112-152">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name.</span></span> <span data-ttu-id="c2112-153">如有必要，請重設密碼。</span><span class="sxs-lookup"><span data-stu-id="c2112-153">If necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="c2112-154">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="c2112-154">Connect and create a table</span></span>
<span data-ttu-id="c2112-155">使用下列程式碼搭配 **CREATE TABLE** SQL 陳述式 (後面接著 **INSERT INTO** SQL 陳述式) 來連線和建立資料表，進而將資料列新增至資料表中。</span><span class="sxs-lookup"><span data-stu-id="c2112-155">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="c2112-156">程式碼會使用 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 物件搭配建構函式 [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize)，以連線至 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="c2112-156">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="c2112-157">然後它會呼叫 [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) 方法來執行 DROP、CREATE TABLE 和 INSERT INTO 命令。</span><span class="sxs-lookup"><span data-stu-id="c2112-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="c2112-158">程式碼會使用 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 類別檢查錯誤。</span><span class="sxs-lookup"><span data-stu-id="c2112-158">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="c2112-159">然後它會呼叫 [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 方法，在終止前關閉連線。</span><span class="sxs-lookup"><span data-stu-id="c2112-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="c2112-160">以您自己的值取代 `host`、`database`、`user` 和 `password` 字串。</span><span class="sxs-lookup"><span data-stu-id="c2112-160">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection to database'

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

## <a name="read-data"></a><span data-ttu-id="c2112-161">讀取資料</span><span class="sxs-lookup"><span data-stu-id="c2112-161">Read data</span></span>
<span data-ttu-id="c2112-162">使用下列程式碼搭配 **SELECT** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c2112-162">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="c2112-163">程式碼會使用 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 物件搭配建構函式 [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize)，以連線至 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="c2112-163">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="c2112-164">然後它會呼叫 [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) 方法來執行 SELECT 命令，並將結果保留在結果集中。</span><span class="sxs-lookup"><span data-stu-id="c2112-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the SELECT command, keeping the results in a result set.</span></span> <span data-ttu-id="c2112-165">結果集的集合會使用 `resultSet.each do` 迴圈反覆運算，並將目前的資料列值保留在 `row` 變數中。</span><span class="sxs-lookup"><span data-stu-id="c2112-165">The result set collection is iterated over using the `resultSet.each do` loop, keeping the current row values in the `row` variable.</span></span> <span data-ttu-id="c2112-166">程式碼會使用 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 類別檢查錯誤。</span><span class="sxs-lookup"><span data-stu-id="c2112-166">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="c2112-167">然後它會呼叫 [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 方法，在終止前關閉連線。</span><span class="sxs-lookup"><span data-stu-id="c2112-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="c2112-168">以您自己的值取代 `host`、`database`、`user` 和 `password` 字串。</span><span class="sxs-lookup"><span data-stu-id="c2112-168">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

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

## <a name="update-data"></a><span data-ttu-id="c2112-169">更新資料</span><span class="sxs-lookup"><span data-stu-id="c2112-169">Update data</span></span>
<span data-ttu-id="c2112-170">使用下列程式碼搭配 **UPDATE** SQL 陳述式來連線和更新資料。</span><span class="sxs-lookup"><span data-stu-id="c2112-170">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="c2112-171">程式碼會使用 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 物件搭配建構函式 [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize)，以連線至 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="c2112-171">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="c2112-172">然後它會呼叫 [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) 方法來執行 UPDATE 命令。</span><span class="sxs-lookup"><span data-stu-id="c2112-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="c2112-173">程式碼會使用 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 類別檢查錯誤。</span><span class="sxs-lookup"><span data-stu-id="c2112-173">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="c2112-174">然後它會呼叫 [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 方法，在終止前關閉連線。</span><span class="sxs-lookup"><span data-stu-id="c2112-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="c2112-175">以您自己的值取代 `host`、`database`、`user` 和 `password` 字串。</span><span class="sxs-lookup"><span data-stu-id="c2112-175">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="c2112-176">刪除資料</span><span class="sxs-lookup"><span data-stu-id="c2112-176">Delete data</span></span>
<span data-ttu-id="c2112-177">使用下列程式碼搭配 **DELETE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c2112-177">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="c2112-178">程式碼會使用 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 物件搭配建構函式 [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize)，以連線至 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="c2112-178">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="c2112-179">然後它會呼叫 [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) 方法來執行 UPDATE 命令。</span><span class="sxs-lookup"><span data-stu-id="c2112-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="c2112-180">程式碼會使用 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 類別檢查錯誤。</span><span class="sxs-lookup"><span data-stu-id="c2112-180">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="c2112-181">然後它會呼叫 [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 方法，在終止前關閉連線。</span><span class="sxs-lookup"><span data-stu-id="c2112-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="c2112-182">以您自己的值取代 `host`、`database`、`user` 和 `password` 字串。</span><span class="sxs-lookup"><span data-stu-id="c2112-182">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="c2112-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2112-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c2112-184">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="c2112-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
