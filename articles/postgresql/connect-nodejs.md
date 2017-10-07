---
title: "從 Node.js PostgreSQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門會提供您可以使用 tooconnect 和查詢 PostgreSQL 資料從 Azure 資料庫的 Node.js 的程式碼範例。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="d308c-103">Azure PostgreSQL 資料庫： 使用 Node.js tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="d308c-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="d308c-104">本快速入門示範如何使用 PostgreSQL 資料庫的 tooconnect tooan Azure [Node.js](https://nodejs.org/)。</span><span class="sxs-lookup"><span data-stu-id="d308c-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="d308c-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="d308c-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="d308c-106">hello 本文章中的步驟假設您已熟悉開發使用 Node.js，且新 tooworking Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d308c-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d308c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="d308c-107">Prerequisites</span></span>
<span data-ttu-id="d308c-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="d308c-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d308c-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="d308c-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="d308c-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="d308c-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="d308c-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="d308c-111">You also need to:</span></span>
- <span data-ttu-id="d308c-112">安裝 [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="d308c-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="d308c-113">安裝 pg 用戶端</span><span class="sxs-lookup"><span data-stu-id="d308c-113">Install pg client</span></span>
<span data-ttu-id="d308c-114">安裝 [pg](https://www.npmjs.com/package/pg)，也就是 PostgreSQL client for Node.js。</span><span class="sxs-lookup"><span data-stu-id="d308c-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="d308c-115">toodo 因此，會執行 javascript hello node 封裝管理員 (npm) 從命令列 tooinstall hello pg 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d308c-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="d308c-116">列出已安裝的 hello 封裝，以確認 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="d308c-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="d308c-117">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="d308c-117">Get connection information</span></span>
<span data-ttu-id="d308c-118">取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d308c-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="d308c-119">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="d308c-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d308c-120">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d308c-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d308c-121">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您剛才建立的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="d308c-122">按一下 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="d308c-122">Click hello server name.</span></span>
4. <span data-ttu-id="d308c-123">選取 hello 伺服器**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="d308c-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="d308c-124">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="d308c-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d308c-125">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="d308c-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="d308c-126">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="d308c-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="d308c-127">Node.js 執行 hello JavaScript 程式碼</span><span class="sxs-lookup"><span data-stu-id="d308c-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="d308c-128">您可能輸入 hello bash 殼層或 windows 命令提示字元之下啟動 Node.js `node`，然後以互動方式執行 hello 範例的 JavaScript 程式碼，藉由複製並貼至 hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="d308c-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="d308c-129">或者，您可能將 hello JavaScript 程式碼儲存成文字檔並啟動`node filename.js`hello 檔案名稱與參數 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="d308c-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d308c-130">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="d308c-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="d308c-131">使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用**CREATE TABLE**和**INSERT INTO** SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d308c-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="d308c-132">hello [pg。用戶端](https://github.com/brianc/node-postgres/wiki/Client)物件是使用的 toointerface 與 hello PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="d308c-133">hello [pg。Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect)函式是使用的 tooestablish hello 連線 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="d308c-134">hello [pg。Client.query()](https://github.com/brianc/node-postgres/wiki/Query)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="d308c-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="d308c-135">Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="d308c-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a><span data-ttu-id="d308c-136">讀取資料</span><span class="sxs-lookup"><span data-stu-id="d308c-136">Read data</span></span>
<span data-ttu-id="d308c-137">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d308c-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="d308c-138">hello [pg。用戶端](https://github.com/brianc/node-postgres/wiki/Client)物件是使用的 toointerface 與 hello PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="d308c-139">hello [pg。Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect)函式是使用的 tooestablish hello 連線 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="d308c-140">hello [pg。Client.query()](https://github.com/brianc/node-postgres/wiki/Query)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="d308c-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="d308c-141">Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="d308c-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a><span data-ttu-id="d308c-142">更新資料</span><span class="sxs-lookup"><span data-stu-id="d308c-142">Update data</span></span>
<span data-ttu-id="d308c-143">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d308c-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="d308c-144">hello [pg。用戶端](https://github.com/brianc/node-postgres/wiki/Client)物件是使用的 toointerface 與 hello PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="d308c-145">hello [pg。Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect)函式是使用的 tooestablish hello 連線 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="d308c-146">hello [pg。Client.query()](https://github.com/brianc/node-postgres/wiki/Query)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="d308c-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="d308c-147">Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="d308c-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a><span data-ttu-id="d308c-148">刪除資料</span><span class="sxs-lookup"><span data-stu-id="d308c-148">Delete data</span></span>
<span data-ttu-id="d308c-149">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d308c-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="d308c-150">hello [pg。用戶端](https://github.com/brianc/node-postgres/wiki/Client)物件是使用的 toointerface 與 hello PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="d308c-151">hello [pg。Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect)函式是使用的 tooestablish hello 連線 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d308c-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="d308c-152">hello [pg。Client.query()](https://github.com/brianc/node-postgres/wiki/Query)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="d308c-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="d308c-153">Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="d308c-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a><span data-ttu-id="d308c-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d308c-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d308c-155">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="d308c-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
