---
title: "用於從 Python MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門會提供數個 Python 程式碼用於 MySQL 的 tooconnect 和查詢資料從 Azure 資料庫的範例。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>Azure 的 MySQL 資料庫： 將 Python tooconnect 和查詢資料
本快速入門示範如何 toouse [Python](https://python.org) tooconnect tooan MySQL 的 Azure 資料庫。 它會從 Mac OS、 Ubuntu Linux 和 Windows 平台的 hello 資料庫中使用 SQL 陳述式 tooquery、 插入、 更新和刪除資料。 本文章中的 hello 步驟假設您熟悉開發使用 Python，並使用新 tooworking 與 MySQL 的 Azure 資料庫。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a>安裝 Python 和 hello MySQL 連接器
安裝[Python](https://www.python.org/downloads/)和 hello [python MySQL 連接器](https://dev.mysql.com/downloads/connector/python/)自己電腦上。 根據您的平台，請依照下列步驟 hello:

### <a name="windows"></a>Windows
1. 從 [python.org](https://www.python.org/downloads/windows/) 下載並安裝 Python 2.7。 
2. 透過啟動 hello 命令提示字元檢查 hello Python 安裝。 執行 hello 命令`C:\python27\python.exe -V`使用 hello 大寫 V 交換器 toosee hello 版本號碼。
3. 用於從 MySQL 安裝 hello Python 連接器[mysql.com](https://dev.mysql.com/downloads/connector/python/)對應的 Python tooyour 版本。

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Python linux (Ubuntu)，通常都會安裝成 hello 預設安裝的一部分。
2. 透過啟動 hello bash 殼層中檢查 hello Python 安裝。 執行 hello 命令`python -V`使用 hello 大寫 V 交換器 toosee hello 版本號碼。
3. 執行 hello 檢查 hello PIP 安裝`pip show pip -V`命令 toosee hello 版本號碼。 
4. PIP 可能包含在某些 Python 版本中。 如果未安裝 PIP，您可能會安裝 hello [PIP] (https://pip.pypa.io/en/stable/installing/) 封裝，執行命令`sudo apt-get install python-pip`。
5. 更新 PIP toohello 最新版本，藉由執行 hello`pip install -U pip`命令。
6. 安裝 Python 和其相依性的 hello MySQL 連接器，使用 hello PIP 命令：

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>MacOS
1. 在 Mac OS Python 通常都會安裝成 hello 預設作業系統安裝的一部分。
2. 透過啟動 hello bash 殼層中檢查 hello Python 安裝。 執行 hello 命令`python -V`使用 hello 大寫 V 交換器 toosee hello 版本號碼。
3. 執行 hello 檢查 hello PIP 安裝`pip show pip -V`命令 toosee hello 版本號碼。
4. PIP 可能包含在某些 Python 版本中。 如果未安裝 PIP，您可能會安裝 hello [PIP](https://pip.pypa.io/en/stable/installing/)封裝。
5. 更新 PIP toohello 最新版本，藉由執行 hello`pip install -U pip`命令。
6. 安裝 Python 和其相依性的 hello MySQL 連接器，使用 hello PIP 命令：

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>取得連線資訊
取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您有 creased，例如 hello 伺服器**myserver4demo**。
3. 按一下伺服器名稱，hello **myserver4demo**。
4. 選取 hello 伺服器**屬性**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for MySQL - 伺服器管理員登入](./media/connect-python/1_server-properties-name-login.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。
   

## <a name="run-python-code"></a>執行 Python 程式碼
- Hello 程式碼貼入文字檔案，並儲存到專案資料夾與檔案副檔名.py，例如 C:\pythonmysql\createtable.py 或 /home/username/pythonmysql/createtable.py hello 檔案
- toorun hello 程式碼中，啟動 hello 命令提示字元，或被殼層。 將目錄切換到專案資料夾 `cd pythonmysql`。 然後輸入 hello python 命令後面 hello 檔案名稱`python createtable.py`toorun hello 應用程式。 在 hello Windows 作業系統，如果找不到 python.exe，您可能會提供 hello 可執行檔的完整路徑 toohello 或 hello Python 路徑加入 hello path 環境變數。 `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>連線、建立資料表及插入資料
使用 hello 下列程式碼 tooconnect toohello 伺服器、 建立資料表，以及載入 hello 資料使用**插入**SQL 陳述式。 

在 hello 程式碼中，會匯入 hello mysql.connector 程式庫。 hello [connect （)](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html)函式是使用的 tooconnect tooAzure 使用 hello 的 MySQL 資料庫[連接引數](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)hello 組態集合中。 hello 程式碼 hello 連接上使用的資料指標和[cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)方法執行 hello 針對 MySQL 資料庫的 SQL 查詢。 

取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a>讀取資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。 

在 hello 程式碼中，會匯入 hello mysql.connector 程式庫。 hello [connect （)](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html)函式是使用的 tooconnect tooAzure 使用 hello 的 MySQL 資料庫[連接引數](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)hello 組態集合中。 hello 程式碼 hello 連接上使用的資料指標和[cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)方法執行 hello 針對 MySQL 資料庫的 SQL 陳述式。 hello 資料列會讀取使用 hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html)方法。 hello 結果集就會保留在集合的資料列和迭代器是使用的 tooloop hello 資料列。

取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。 

在 hello 程式碼中，會匯入 hello mysql.connector 程式庫。  hello [connect （)](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html)函式是使用的 tooconnect tooAzure 使用 hello 的 MySQL 資料庫[連接引數](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)hello 組態集合中。 hello 程式碼 hello 連接上使用的資料指標和[cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)方法執行 hello 針對 MySQL 資料庫的 SQL 陳述式。 

取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼 tooconnect 並移除資料使用**刪除**SQL 陳述式。 

在 hello 程式碼中，會匯入 hello mysql.connector 程式庫。  hello [connect （)](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html)函式是使用的 tooconnect tooAzure 使用 hello 的 MySQL 資料庫[連接引數](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)hello 組態集合中。 hello 程式碼 hello 連接上使用的資料指標和[cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)方法執行 hello 針對 MySQL 資料庫的 SQL 查詢。 

取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [使用匯出和匯入來移轉資料庫](./concepts-migrate-import-export.md)
