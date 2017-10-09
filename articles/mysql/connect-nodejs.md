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
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>Azure 資料庫的 MySQL： 使用 Node.js tooconnect 和查詢資料
本快速入門示範如何使用 MySQL 資料庫的 tooconnect tooan Azure [Node.js](https://nodejs.org/)從 Windows、 Ubuntu Linux 和 Mac 平台。 它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。 hello 本文章中的步驟假設您已熟悉開發使用 Node.js，且新 tooworking 與 MySQL 的 Azure 資料庫。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-cli.md)

您也需要：
- 安裝 hello [Node.js](https://nodejs.org)執行階段。
- 安裝[mysql2](https://www.npmjs.com/package/mysql2)封裝 tooconnect tooMySQL 從 hello Node.js 應用程式。 

## <a name="install-nodejs-and-hello-mysql-connector"></a>安裝 Node.js 和 hello MySQL 連接器
根據您的平台，請遵循 hello 適當的指示 tooinstall Node.js。 使用 npm tooinstall hello mysql2 封裝和其相依性到專案資料夾中。

### <a name="windows"></a>**Windows**
1. 請瀏覽 hello [Node.js 下載頁面](https://nodejs.org/en/download/)和選取您想要的 Windows 安裝程式選項。
2. 建立本機專案資料夾，例如 `nodejsmysql`。 
3. 啟動 hello 命令提示字元，並在 cd 至 hello 專案資料夾中例如`cd c:\nodejsmysql\`
4. 遇到 hello 專案資料夾中的 hello NPM 工具 tooinstall hello mysql2 程式庫。

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. 藉由檢查 hello 確認 hello 安裝`npm list`輸出文字`mysql2@1.3.5`。

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. Hello 執行的下列命令 tooinstall **Node.js**和**npm** for Node.js hello 封裝管理員。

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. 專案資料夾執行下列命令 toomake hello`mysqlnodejs`和 hello mysql2 封裝安裝到該資料夾。

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. 藉由檢查 npm 清單的輸出文字確認 hello 安裝`mysql2@1.3.5`。

### <a name="mac-os"></a>**Mac OS**
1. 輸入下列命令 tooinstall hello **brew**、 Mac OS X 的方便使用封裝管理員和**Node.js**。

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. 專案資料夾執行下列命令 toomake hello`mysqlnodejs`和 hello mysql2 封裝安裝到該資料夾。

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. 藉由檢查 hello 確認 hello 安裝`npm list`輸出文字`mysql2@1.3.6`。 hello 版本號碼可能有所不同發行新的修補程式。

## <a name="get-connection-information"></a>取得連線資訊
取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. Hello 左窗格中，按一下 **所有資源**，然後搜尋您所建立的 hello server (例如， **myserver4demo**)。
3. 按一下伺服器名稱，hello **myserver4demo**。
4. 選取 hello 伺服器**屬性**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for MySQL - 伺服器管理員登入](./media/connect-nodejs/1_server-properties-name-login.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。

## <a name="running-hello-javascript-code-in-nodejs"></a>Node.js 執行 hello JavaScript 程式碼
1. Hello JavaScript 程式碼貼入文字檔案，並儲存到專案資料夾與檔案副檔名.js，例如 C:\nodejsmysql\createtable.js 或 /home/username/nodejsmysql/createtable.js
2. 啟動 hello 命令提示字元，或被殼層。 將目錄切換到專案資料夾 `cd nodejsmysql`。
3. toorun hello 應用程式中，輸入 hello 節點命令後面 hello 檔案名稱，例如`node createtable.js`。
4. 在 Windows 中，如果 hello node 應用程式不在您的環境變數路徑，您可能需要 toouse hello 完整路徑 toolaunch hello node 應用程式例如`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>連線、建立資料表及插入資料
使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用**CREATE TABLE**和**INSERT INTO** SQL 陳述式。

hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 toointerface 與 hello MySQL 伺服器。 hello [connect （)](https://github.com/mysqljs/mysql#establishing-connections)函式是使用的 tooestablish hello 連線 toohello 伺服器。 hello [query （)](https://github.com/mysqljs/mysql#performing-queries)函式是使用的 tooexecute hello SQL 查詢，MySQL 資料庫。 

取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。

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

## <a name="read-data"></a>讀取資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。 

hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 toointerface 與 hello MySQL 伺服器。 hello [connect （)](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 tooestablish hello 連接 toohello 伺服器。 hello [query （)](https://github.com/mysqljs/mysql#performing-queries)方法是使用的 tooexecute hello SQL 查詢，MySQL 資料庫。 hello 結果陣列是使用的 toohold hello hello 查詢結果。

取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。

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

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**更新**SQL 陳述式。 

hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 toointerface 與 hello MySQL 伺服器。 hello [connect （)](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 tooestablish hello 連接 toohello 伺服器。 hello [query （)](https://github.com/mysqljs/mysql#performing-queries)方法是使用的 tooexecute hello SQL 查詢，MySQL 資料庫。 

取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。

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

## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。 

hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 toointerface 與 hello MySQL 伺服器。 hello [connect （)](https://github.com/mysqljs/mysql#establishing-connections)方法是使用的 tooestablish hello 連接 toohello 伺服器。 hello [query （)](https://github.com/mysqljs/mysql#performing-queries)方法是使用的 tooexecute hello SQL 查詢，MySQL 資料庫。 

取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。

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

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [使用匯出和匯入來移轉資料庫](./concepts-migrate-import-export.md)
