---
title: "用於從 Node.js MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門會提供數個 Node.js 的程式碼範例，您可以使用 tooconnect 和查詢資料從 Azure 資料庫的 MySQL。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="0a8a7-103">Azure 資料庫的 MySQL： 使用 Node.js tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="0a8a7-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="0a8a7-104">本快速入門示範如何使用 MySQL 資料庫的 tooconnect tooan Azure [Node.js](https://nodejs.org/)從 Windows、 Ubuntu Linux 和 Mac 平台。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="0a8a7-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="0a8a7-106">hello 本文章中的步驟假設您已熟悉開發使用 Node.js，且新 tooworking 與 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a8a7-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a8a7-107">Prerequisites</span></span>
<span data-ttu-id="0a8a7-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="0a8a7-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="0a8a7-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="0a8a7-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="0a8a7-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="0a8a7-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="0a8a7-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="0a8a7-111">You also need to:</span></span>
- <span data-ttu-id="0a8a7-112">安裝 hello [Node.js](https://nodejs.org)執行階段。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="0a8a7-113">安裝[mysql2](https://www.npmjs.com/package/mysql2)封裝 tooconnect tooMySQL 從 hello Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="0a8a7-114">安裝 Node.js 和 hello MySQL 連接器</span><span class="sxs-lookup"><span data-stu-id="0a8a7-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="0a8a7-115">根據您的平台，請遵循 hello 適當的指示 tooinstall Node.js。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="0a8a7-116">使用 npm tooinstall hello mysql2 封裝和其相依性到專案資料夾中。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="0a8a7-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="0a8a7-117">**Windows**</span></span>
1. <span data-ttu-id="0a8a7-118">請瀏覽 hello [Node.js 下載頁面](https://nodejs.org/en/download/)和選取您想要的 Windows 安裝程式選項。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="0a8a7-119">建立本機專案資料夾，例如 `nodejsmysql`。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="0a8a7-120">啟動 hello 命令提示字元，並在 cd 至 hello 專案資料夾中例如`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="0a8a7-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="0a8a7-121">遇到 hello 專案資料夾中的 hello NPM 工具 tooinstall hello mysql2 程式庫。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="0a8a7-122">藉由檢查 hello 確認 hello 安裝`npm list`輸出文字`mysql2@1.3.5`。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="0a8a7-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="0a8a7-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="0a8a7-124">Hello 執行的下列命令 tooinstall **Node.js**和**npm** for Node.js hello 封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="0a8a7-125">專案資料夾執行下列命令 toomake hello`mysqlnodejs`和 hello mysql2 封裝安裝到該資料夾。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="0a8a7-126">藉由檢查 npm 清單的輸出文字確認 hello 安裝`mysql2@1.3.5`。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="0a8a7-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="0a8a7-127">**Mac OS**</span></span>
1. <span data-ttu-id="0a8a7-128">輸入下列命令 tooinstall hello **brew**、 Mac OS X 的方便使用封裝管理員和**Node.js**。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="0a8a7-129">專案資料夾執行下列命令 toomake hello`mysqlnodejs`和 hello mysql2 封裝安裝到該資料夾。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="0a8a7-130">藉由檢查 hello 確認 hello 安裝`npm list`輸出文字`mysql2@1.3.6`。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="0a8a7-131">hello 版本號碼可能有所不同發行新的修補程式。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0a8a7-132">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="0a8a7-132">Get connection information</span></span>
<span data-ttu-id="0a8a7-133">取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="0a8a7-134">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0a8a7-135">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0a8a7-136">Hello 左窗格中，按一下 **所有資源**，然後搜尋您所建立的 hello server (例如， **myserver4demo**)。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="0a8a7-137">按一下伺服器名稱，hello **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="0a8a7-138">選取 hello 伺服器**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="0a8a7-139">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="0a8a7-140">![Azure Database for MySQL - 伺服器管理員登入](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="0a8a7-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="0a8a7-141">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="0a8a7-142">Node.js 執行 hello JavaScript 程式碼</span><span class="sxs-lookup"><span data-stu-id="0a8a7-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="0a8a7-143">Hello JavaScript 程式碼貼入文字檔案，並儲存到專案資料夾與檔案副檔名.js，例如 C:\nodejsmysql\createtable.js 或 /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="0a8a7-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="0a8a7-144">啟動 hello 命令提示字元，或被殼層。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="0a8a7-145">將目錄切換到專案資料夾 `cd nodejsmysql`。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="0a8a7-146">toorun hello 應用程式中，輸入 hello 節點命令後面 hello 檔案名稱，例如`node createtable.js`。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="0a8a7-147">在 Windows 中，如果 hello node 應用程式不在您的環境變數路徑，您可能需要 toouse hello 完整路徑 toolaunch hello node 應用程式例如`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="0a8a7-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="0a8a7-148">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="0a8a7-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="0a8a7-149">使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用**CREATE TABLE**和**INSERT INTO** SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="0a8a7-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 toointerface 與 hello MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="0a8a7-151">hello [connect （)](https://github.com/mysqljs/mysql#establishing-connections)函式是使用的 tooestablish hello 連線 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="0a8a7-152">hello [query （)](https://github.com/mysqljs/mysql#performing-queries)函式是使用的 tooexecute hello SQL 查詢，MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="0a8a7-153">取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="0a8a7-154">讀取資料</span><span class="sxs-lookup"><span data-stu-id="0a8a7-154">Read data</span></span>
<span data-ttu-id="0a8a7-155">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="0a8a7-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 toointerface 與 hello MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="0a8a7-157">hello [connect （)](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 tooestablish hello 連接 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="0a8a7-158">hello [query （)](https://github.com/mysqljs/mysql#performing-queries)方法是使用的 tooexecute hello SQL 查詢，MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="0a8a7-159">hello 結果陣列是使用的 toohold hello hello 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="0a8a7-160">取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="0a8a7-161">更新資料</span><span class="sxs-lookup"><span data-stu-id="0a8a7-161">Update data</span></span>
<span data-ttu-id="0a8a7-162">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="0a8a7-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 toointerface 與 hello MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="0a8a7-164">hello [connect （)](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 tooestablish hello 連接 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="0a8a7-165">hello [query （)](https://github.com/mysqljs/mysql#performing-queries)方法是使用的 tooexecute hello SQL 查詢，MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="0a8a7-166">取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="0a8a7-167">刪除資料</span><span class="sxs-lookup"><span data-stu-id="0a8a7-167">Delete data</span></span>
<span data-ttu-id="0a8a7-168">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="0a8a7-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 toointerface 與 hello MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="0a8a7-170">hello [connect （)](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 tooestablish hello 連接 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="0a8a7-171">hello [query （)](https://github.com/mysqljs/mysql#performing-queries)方法是使用的 tooexecute hello SQL 查詢，MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="0a8a7-172">取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。</span><span class="sxs-lookup"><span data-stu-id="0a8a7-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="0a8a7-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a8a7-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0a8a7-174">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="0a8a7-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
