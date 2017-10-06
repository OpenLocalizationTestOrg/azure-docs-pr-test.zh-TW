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
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="6b1d6-103">Azure PostgreSQL 資料庫： 使用 Ruby tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="6b1d6-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="6b1d6-104">本快速入門示範如何使用 PostgreSQL 資料庫的 tooconnect tooan Azure [Ruby](https://www.ruby-lang.org)應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="6b1d6-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="6b1d6-106">本文假設您熟悉開發使用 Ruby，但是，您就可以新增 tooworking Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b1d6-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="6b1d6-107">Prerequisites</span></span>
<span data-ttu-id="6b1d6-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="6b1d6-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="6b1d6-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="6b1d6-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="6b1d6-110">建立 DB - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6b1d6-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="6b1d6-111">安裝 Ruby</span><span class="sxs-lookup"><span data-stu-id="6b1d6-111">Install Ruby</span></span>
<span data-ttu-id="6b1d6-112">在自己的電腦上安裝 Ruby。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="6b1d6-113">Windows</span><span class="sxs-lookup"><span data-stu-id="6b1d6-113">Windows</span></span>
- <span data-ttu-id="6b1d6-114">下載並安裝 hello 最新版本[Ruby](http://rubyinstaller.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="6b1d6-115">在 hello 完成畫面 hello MSI 安裝程式，請檢查 hello 方塊，指出 「 執行 'ridk install' tooinstall MSYS2 和開發工具鏈。 」</span><span class="sxs-lookup"><span data-stu-id="6b1d6-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="6b1d6-116">然後按一下 **完成**toolaunch hello 下一個安裝程式。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="6b1d6-117">hello RubyInstaller2 適用於 Windows 的安裝程式會啟動。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="6b1d6-118">輸入 2 tooinstall hello MSYS2 儲存機制更新。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="6b1d6-119">它完成並傳回 toohello 安裝提示之後，關閉 hello 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="6b1d6-120">從 hello [開始] 功能表中啟動新的命令提示字元 (cmd)。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="6b1d6-121">測試 hello 拼音安裝`ruby -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="6b1d6-122">測試 hello 健身安裝`gem -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="6b1d6-123">建置執行 hello 命令使用寶石的 Ruby hello PostgreSQL 模組`gem install pg`。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="6b1d6-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="6b1d6-124">MacOS</span></span>
- <span data-ttu-id="6b1d6-125">安裝執行 hello 命令使用 Homebrew Ruby `brew install ruby`。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="6b1d6-126">如需其他安裝選項，請參閱 hello Ruby[安裝文件集](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="6b1d6-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="6b1d6-127">測試 hello 拼音安裝`ruby -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="6b1d6-128">測試 hello 健身安裝`gem -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="6b1d6-129">建置執行 hello 命令使用寶石的 Ruby hello PostgreSQL 模組`gem install pg`。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="6b1d6-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="6b1d6-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="6b1d6-131">執行 hello 命令來安裝 Ruby `sudo apt-get install ruby-full`。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="6b1d6-132">如需其他安裝選項，請參閱 hello Ruby[安裝文件集](https://www.ruby-lang.org/en/documentation/installation/)。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="6b1d6-133">測試 hello 拼音安裝`ruby -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="6b1d6-134">安裝執行 hello 命令 hello 最新更新健身`sudo gem update --system`。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="6b1d6-135">測試 hello 健身安裝`gem -v`toosee hello 版本安裝。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="6b1d6-136">執行 hello 命令來安裝 hello gcc、 樣式及其他建置工具`sudo apt-get install build-essential`。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="6b1d6-137">執行 hello 命令來安裝 hello PostgreSQL 程式庫`sudo apt-get install libpq-dev`。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="6b1d6-138">建置執行 hello 命令使用健身 hello 拼音 pg 模組`sudo gem install pg`。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="6b1d6-139">執行 Ruby 程式碼</span><span class="sxs-lookup"><span data-stu-id="6b1d6-139">Run Ruby code</span></span> 
- <span data-ttu-id="6b1d6-140">Hello 程式碼儲存到文字檔，並儲存 hello 檔案到專案資料夾與檔案延伸模組需要.rb，例如`C:\rubypostgres\read.rb`或`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="6b1d6-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="6b1d6-141">toorun hello 程式碼中，啟動 hello 命令提示字元，或被殼層。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="6b1d6-142">將目錄切換到您的專案資料夾`cd rubypostgres`，然後輸入 hello 命令`ruby read.rb`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="6b1d6-143">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="6b1d6-143">Get connection information</span></span>
<span data-ttu-id="6b1d6-144">取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="6b1d6-145">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="6b1d6-146">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6b1d6-147">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="6b1d6-148">按一下伺服器名稱，hello **mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="6b1d6-149">選取 hello 伺服器**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="6b1d6-150">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="6b1d6-151">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="6b1d6-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="6b1d6-152">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="6b1d6-153">如有需要，重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="6b1d6-154">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="6b1d6-154">Connect and create a table</span></span>
<span data-ttu-id="6b1d6-155">使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式，後面接著**INSERT INTO** hello 資料表的 SQL 陳述式 tooadd 資料列。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="6b1d6-156">hello 程式碼會使用[PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection)具有建構函式物件[new （)](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="6b1d6-157">然後它會呼叫方法[exec （)](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello 卸除、 CREATE TABLE 和 INSERT INTO 命令。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="6b1d6-158">hello 程式碼會檢查是否有錯誤使用 hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error)類別。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="6b1d6-159">然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello 連線後，再終止。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="6b1d6-160">取代 hello `host`， `database`， `user`，和`password`字串以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
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

## <a name="read-data"></a><span data-ttu-id="6b1d6-161">讀取資料</span><span class="sxs-lookup"><span data-stu-id="6b1d6-161">Read data</span></span>
<span data-ttu-id="6b1d6-162">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="6b1d6-163">hello 程式碼會使用[PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection)具有建構函式物件[new （)](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="6b1d6-164">然後它會呼叫方法[exec （)](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT 命令，將 hello 結果保留在結果集。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="6b1d6-165">hello 結果集的集合會一直重複使用 hello`resultSet.each do`迴圈，hello 目前資料列的值保持在 hello`row`變數。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="6b1d6-166">hello 程式碼會檢查是否有錯誤使用 hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error)類別。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="6b1d6-167">然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello 連線後，再終止。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="6b1d6-168">取代 hello `host`， `database`， `user`，和`password`字串以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="6b1d6-169">更新資料</span><span class="sxs-lookup"><span data-stu-id="6b1d6-169">Update data</span></span>
<span data-ttu-id="6b1d6-170">使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="6b1d6-171">hello 程式碼會使用[PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection)具有建構函式物件[new （)](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="6b1d6-172">然後它會呼叫方法[exec （)](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello 更新命令。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="6b1d6-173">hello 程式碼會檢查是否有錯誤使用 hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error)類別。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="6b1d6-174">然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello 連線後，再終止。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="6b1d6-175">取代 hello `host`， `database`， `user`，和`password`字串以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="6b1d6-176">刪除資料</span><span class="sxs-lookup"><span data-stu-id="6b1d6-176">Delete data</span></span>
<span data-ttu-id="6b1d6-177">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="6b1d6-178">hello 程式碼會使用[PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection)具有建構函式物件[new （)](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="6b1d6-179">然後它會呼叫方法[exec （)](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello 更新命令。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="6b1d6-180">hello 程式碼會檢查是否有錯誤使用 hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error)類別。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="6b1d6-181">然後它會呼叫方法[close （)](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello 連線後，再終止。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="6b1d6-182">取代 hello `host`， `database`， `user`，和`password`字串以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="6b1d6-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="6b1d6-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b1d6-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6b1d6-184">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="6b1d6-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
