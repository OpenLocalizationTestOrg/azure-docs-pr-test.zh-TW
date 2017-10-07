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
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Azure PostgreSQL 資料庫： 使用 Node.js tooconnect 和查詢資料
本快速入門示範如何使用 PostgreSQL 資料庫的 tooconnect tooan Azure [Node.js](https://nodejs.org/)。 它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。 hello 本文章中的步驟假設您已熟悉開發使用 Node.js，且新 tooworking Azure PostgreSQL 資料庫。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [建立 DB - 入口網站](quickstart-create-server-database-portal.md)
- [建立 DB - CLI](quickstart-create-server-database-azure-cli.md)

您也需要：
- 安裝 [Node.js](https://nodejs.org)

## <a name="install-pg-client"></a>安裝 pg 用戶端
安裝 [pg](https://www.npmjs.com/package/pg)，也就是 PostgreSQL client for Node.js。

toodo 因此，會執行 javascript hello node 封裝管理員 (npm) 從命令列 tooinstall hello pg 用戶端。
```bash
npm install pg
```

列出已安裝的 hello 封裝，以確認 hello 安裝。
```bash
npm list
```

## <a name="get-connection-information"></a>取得連線資訊
取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您剛才建立的 hello 伺服器。
3. 按一下 hello 伺服器名稱。
4. 選取 hello 伺服器**概觀**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-nodejs/1-connection-string.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。

## <a name="running-hello-javascript-code-in-nodejs"></a>Node.js 執行 hello JavaScript 程式碼
您可能輸入 hello bash 殼層或 windows 命令提示字元之下啟動 Node.js `node`，然後以互動方式執行 hello 範例的 JavaScript 程式碼，藉由複製並貼至 hello 提示字元。 或者，您可能將 hello JavaScript 程式碼儲存成文字檔並啟動`node filename.js`hello 檔案名稱與參數 toorun 它。

## <a name="connect-create-table-and-insert-data"></a>連線、建立資料表及插入資料
使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用**CREATE TABLE**和**INSERT INTO** SQL 陳述式。
hello [pg。用戶端](https://github.com/brianc/node-postgres/wiki/Client)物件是使用的 toointerface 與 hello PostgreSQL 伺服器。 hello [pg。Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect)函式是使用的 tooestablish hello 連線 toohello 伺服器。 hello [pg。Client.query()](https://github.com/brianc/node-postgres/wiki/Query)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。 

Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。

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

## <a name="read-data"></a>讀取資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。 hello [pg。用戶端](https://github.com/brianc/node-postgres/wiki/Client)物件是使用的 toointerface 與 hello PostgreSQL 伺服器。 hello [pg。Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect)函式是使用的 tooestablish hello 連線 toohello 伺服器。 hello [pg。Client.query()](https://github.com/brianc/node-postgres/wiki/Query)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。 

Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。 

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

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**更新**SQL 陳述式。 hello [pg。用戶端](https://github.com/brianc/node-postgres/wiki/Client)物件是使用的 toointerface 與 hello PostgreSQL 伺服器。 hello [pg。Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect)函式是使用的 tooestablish hello 連線 toohello 伺服器。 hello [pg。Client.query()](https://github.com/brianc/node-postgres/wiki/Query)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。 

Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。 

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

## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。 hello [pg。用戶端](https://github.com/brianc/node-postgres/wiki/Client)物件是使用的 toointerface 與 hello PostgreSQL 伺服器。 hello [pg。Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect)函式是使用的 tooestablish hello 連線 toohello 伺服器。 hello [pg。Client.query()](https://github.com/brianc/node-postgres/wiki/Query)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。 

Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。 

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

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [使用匯出和匯入來移轉資料庫](./howto-migrate-using-export-and-import.md)
