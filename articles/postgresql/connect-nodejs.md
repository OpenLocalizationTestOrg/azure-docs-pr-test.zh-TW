---
title: "從 Node.js 連線至 Azure Database for PostgreSQL | Microsoft Docs"
description: "本快速入門提供 Node.js 程式碼範例，供您在從 Azure Database for PostgreSQL 連線及查詢資料時使用。"
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
ms.openlocfilehash: f6c98833c73b70bcf1f8ca53596a34f09807b276
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="62e5c-103">Azure Database for PostgreSQL︰使用 Node.js 連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="62e5c-103">Azure Database for PostgreSQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="62e5c-104">本快速入門示範如何使用 [Node.js](https://nodejs.org/) 來連線到 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="62e5c-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="62e5c-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="62e5c-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="62e5c-106">本文中的步驟假設您已熟悉使用 Node.js 進行開發，但不熟悉 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="62e5c-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62e5c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="62e5c-107">Prerequisites</span></span>
<span data-ttu-id="62e5c-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="62e5c-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="62e5c-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="62e5c-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="62e5c-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="62e5c-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="62e5c-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="62e5c-111">You also need to:</span></span>
- <span data-ttu-id="62e5c-112">安裝 [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="62e5c-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="62e5c-113">安裝 pg 用戶端</span><span class="sxs-lookup"><span data-stu-id="62e5c-113">Install pg client</span></span>
<span data-ttu-id="62e5c-114">安裝 [pg](https://www.npmjs.com/package/pg)，也就是 PostgreSQL client for Node.js。</span><span class="sxs-lookup"><span data-stu-id="62e5c-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="62e5c-115">若要這樣做，請從命令列執行適用於 JavaScript 的節點套件管理員 (npm) 以安裝 pg 用戶端。</span><span class="sxs-lookup"><span data-stu-id="62e5c-115">To do so, run the node package manager (npm) for JavaScript from your command line to install the pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="62e5c-116">列出已安裝的套件以確認安裝。</span><span class="sxs-lookup"><span data-stu-id="62e5c-116">Verify the installation by listing the packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="62e5c-117">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="62e5c-117">Get connection information</span></span>
<span data-ttu-id="62e5c-118">取得連線到 Azure Database for PostgreSQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="62e5c-118">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="62e5c-119">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="62e5c-119">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="62e5c-120">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="62e5c-120">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="62e5c-121">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您剛建立的伺服器。</span><span class="sxs-lookup"><span data-stu-id="62e5c-121">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created.</span></span>
3. <span data-ttu-id="62e5c-122">按一下伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="62e5c-122">Click the server name.</span></span>
4. <span data-ttu-id="62e5c-123">選取伺服器的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="62e5c-123">Select the server's **Overview** page.</span></span> <span data-ttu-id="62e5c-124">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="62e5c-124">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="62e5c-125">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="62e5c-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="62e5c-126">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="62e5c-126">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="62e5c-127">在 Node.js 中執行 JavaScript 程式碼</span><span class="sxs-lookup"><span data-stu-id="62e5c-127">Running the JavaScript code in Node.js</span></span>
<span data-ttu-id="62e5c-128">您可藉由輸入 `node` 以從 bash shell 或 Windows 命令提示字元啟動 Node.js，然後複製範例 JavaScript 程式碼並將其貼至提示字元，以互動方式執行。</span><span class="sxs-lookup"><span data-stu-id="62e5c-128">You may launch Node.js from the bash shell or windows command prompt by typing `node`, then run the example JavaScript code interactively by copy and pasting it onto the prompt.</span></span> <span data-ttu-id="62e5c-129">或者，您可以將 JavaScript 程式碼儲存成文字檔並以檔案名稱作為參數來啟動 `node filename.js`，進而執行它。</span><span class="sxs-lookup"><span data-stu-id="62e5c-129">Alternatively, you may save the JavaScript code into a text file and launch `node filename.js` with the file name as a parameter to run it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="62e5c-130">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="62e5c-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="62e5c-131">使用下列程式碼搭配 **CREATE TABLE** 和 **INSERT INTO** SQL 陳述式來連線和載入資料。</span><span class="sxs-lookup"><span data-stu-id="62e5c-131">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="62e5c-132">[pg.Client](https://github.com/brianc/node-postgres/wiki/Client) 物件用來與 PostgreSQL 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="62e5c-132">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="62e5c-133">[pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) 函式用來建立伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="62e5c-133">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="62e5c-134">[pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) 函式用來對 PostgreSQL 資料庫執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="62e5c-134">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="62e5c-135">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="62e5c-135">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="62e5c-136">讀取資料</span><span class="sxs-lookup"><span data-stu-id="62e5c-136">Read data</span></span>
<span data-ttu-id="62e5c-137">使用下列程式碼搭配 **SELECT** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="62e5c-137">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="62e5c-138">[pg.Client](https://github.com/brianc/node-postgres/wiki/Client) 物件用來與 PostgreSQL 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="62e5c-138">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="62e5c-139">[pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) 函式用來建立伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="62e5c-139">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="62e5c-140">[pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) 函式用來對 PostgreSQL 資料庫執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="62e5c-140">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="62e5c-141">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="62e5c-141">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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
  
    console.log(`Running query to PostgreSQL server: ${config.host}`);

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

## <a name="update-data"></a><span data-ttu-id="62e5c-142">更新資料</span><span class="sxs-lookup"><span data-stu-id="62e5c-142">Update data</span></span>
<span data-ttu-id="62e5c-143">使用下列程式碼搭配 **UPDATE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="62e5c-143">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="62e5c-144">[pg.Client](https://github.com/brianc/node-postgres/wiki/Client) 物件用來與 PostgreSQL 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="62e5c-144">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="62e5c-145">[pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) 函式用來建立伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="62e5c-145">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="62e5c-146">[pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) 函式用來對 PostgreSQL 資料庫執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="62e5c-146">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="62e5c-147">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="62e5c-147">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="62e5c-148">刪除資料</span><span class="sxs-lookup"><span data-stu-id="62e5c-148">Delete data</span></span>
<span data-ttu-id="62e5c-149">使用下列程式碼搭配 **DELETE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="62e5c-149">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="62e5c-150">[pg.Client](https://github.com/brianc/node-postgres/wiki/Client) 物件用來與 PostgreSQL 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="62e5c-150">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="62e5c-151">[pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) 函式用來建立伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="62e5c-151">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="62e5c-152">[pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) 函式用來對 PostgreSQL 資料庫執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="62e5c-152">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="62e5c-153">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="62e5c-153">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="62e5c-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62e5c-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="62e5c-155">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="62e5c-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
