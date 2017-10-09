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
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="7636b-103">Azure 的 MySQL 資料庫： 將 Python tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="7636b-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="7636b-104">本快速入門示範如何 toouse [Python](https://python.org) tooconnect tooan MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7636b-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="7636b-105">它會從 Mac OS、 Ubuntu Linux 和 Windows 平台的 hello 資料庫中使用 SQL 陳述式 tooquery、 插入、 更新和刪除資料。</span><span class="sxs-lookup"><span data-stu-id="7636b-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="7636b-106">本文章中的 hello 步驟假設您熟悉開發使用 Python，並使用新 tooworking 與 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7636b-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7636b-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="7636b-107">Prerequisites</span></span>
<span data-ttu-id="7636b-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="7636b-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="7636b-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="7636b-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="7636b-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="7636b-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="7636b-111">安裝 Python 和 hello MySQL 連接器</span><span class="sxs-lookup"><span data-stu-id="7636b-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="7636b-112">安裝[Python](https://www.python.org/downloads/)和 hello [python MySQL 連接器](https://dev.mysql.com/downloads/connector/python/)自己電腦上。</span><span class="sxs-lookup"><span data-stu-id="7636b-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="7636b-113">根據您的平台，請依照下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="7636b-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="7636b-114">Windows</span><span class="sxs-lookup"><span data-stu-id="7636b-114">Windows</span></span>
1. <span data-ttu-id="7636b-115">從 [python.org](https://www.python.org/downloads/windows/) 下載並安裝 Python 2.7。</span><span class="sxs-lookup"><span data-stu-id="7636b-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="7636b-116">透過啟動 hello 命令提示字元檢查 hello Python 安裝。</span><span class="sxs-lookup"><span data-stu-id="7636b-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="7636b-117">執行 hello 命令`C:\python27\python.exe -V`使用 hello 大寫 V 交換器 toosee hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="7636b-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="7636b-118">用於從 MySQL 安裝 hello Python 連接器[mysql.com](https://dev.mysql.com/downloads/connector/python/)對應的 Python tooyour 版本。</span><span class="sxs-lookup"><span data-stu-id="7636b-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="7636b-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="7636b-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="7636b-120">Python linux (Ubuntu)，通常都會安裝成 hello 預設安裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="7636b-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="7636b-121">透過啟動 hello bash 殼層中檢查 hello Python 安裝。</span><span class="sxs-lookup"><span data-stu-id="7636b-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="7636b-122">執行 hello 命令`python -V`使用 hello 大寫 V 交換器 toosee hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="7636b-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="7636b-123">執行 hello 檢查 hello PIP 安裝`pip show pip -V`命令 toosee hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="7636b-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="7636b-124">PIP 可能包含在某些 Python 版本中。</span><span class="sxs-lookup"><span data-stu-id="7636b-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="7636b-125">如果未安裝 PIP，您可能會安裝 hello [PIP] (https://pip.pypa.io/en/stable/installing/) 封裝，執行命令`sudo apt-get install python-pip`。</span><span class="sxs-lookup"><span data-stu-id="7636b-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="7636b-126">更新 PIP toohello 最新版本，藉由執行 hello`pip install -U pip`命令。</span><span class="sxs-lookup"><span data-stu-id="7636b-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="7636b-127">安裝 Python 和其相依性的 hello MySQL 連接器，使用 hello PIP 命令：</span><span class="sxs-lookup"><span data-stu-id="7636b-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="7636b-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="7636b-128">MacOS</span></span>
1. <span data-ttu-id="7636b-129">在 Mac OS Python 通常都會安裝成 hello 預設作業系統安裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="7636b-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="7636b-130">透過啟動 hello bash 殼層中檢查 hello Python 安裝。</span><span class="sxs-lookup"><span data-stu-id="7636b-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="7636b-131">執行 hello 命令`python -V`使用 hello 大寫 V 交換器 toosee hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="7636b-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="7636b-132">執行 hello 檢查 hello PIP 安裝`pip show pip -V`命令 toosee hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="7636b-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="7636b-133">PIP 可能包含在某些 Python 版本中。</span><span class="sxs-lookup"><span data-stu-id="7636b-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="7636b-134">如果未安裝 PIP，您可能會安裝 hello [PIP](https://pip.pypa.io/en/stable/installing/)封裝。</span><span class="sxs-lookup"><span data-stu-id="7636b-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="7636b-135">更新 PIP toohello 最新版本，藉由執行 hello`pip install -U pip`命令。</span><span class="sxs-lookup"><span data-stu-id="7636b-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="7636b-136">安裝 Python 和其相依性的 hello MySQL 連接器，使用 hello PIP 命令：</span><span class="sxs-lookup"><span data-stu-id="7636b-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="7636b-137">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="7636b-137">Get connection information</span></span>
<span data-ttu-id="7636b-138">取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7636b-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="7636b-139">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="7636b-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="7636b-140">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="7636b-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7636b-141">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您有 creased，例如 hello 伺服器**myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="7636b-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="7636b-142">按一下伺服器名稱，hello **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="7636b-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="7636b-143">選取 hello 伺服器**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="7636b-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="7636b-144">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="7636b-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="7636b-145">![Azure Database for MySQL - 伺服器管理員登入](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="7636b-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="7636b-146">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="7636b-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="7636b-147">執行 Python 程式碼</span><span class="sxs-lookup"><span data-stu-id="7636b-147">Run Python Code</span></span>
- <span data-ttu-id="7636b-148">Hello 程式碼貼入文字檔案，並儲存到專案資料夾與檔案副檔名.py，例如 C:\pythonmysql\createtable.py 或 /home/username/pythonmysql/createtable.py hello 檔案</span><span class="sxs-lookup"><span data-stu-id="7636b-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="7636b-149">toorun hello 程式碼中，啟動 hello 命令提示字元，或被殼層。</span><span class="sxs-lookup"><span data-stu-id="7636b-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="7636b-150">將目錄切換到專案資料夾 `cd pythonmysql`。</span><span class="sxs-lookup"><span data-stu-id="7636b-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="7636b-151">然後輸入 hello python 命令後面 hello 檔案名稱`python createtable.py`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7636b-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="7636b-152">在 hello Windows 作業系統，如果找不到 python.exe，您可能會提供 hello 可執行檔的完整路徑 toohello 或 hello Python 路徑加入 hello path 環境變數。</span><span class="sxs-lookup"><span data-stu-id="7636b-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="7636b-153">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="7636b-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="7636b-154">使用 hello 下列程式碼 tooconnect toohello 伺服器、 建立資料表，以及載入 hello 資料使用**插入**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7636b-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="7636b-155">在 hello 程式碼中，會匯入 hello mysql.connector 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7636b-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="7636b-156">hello [connect （)](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html)函式是使用的 tooconnect tooAzure 使用 hello 的 MySQL 資料庫[連接引數](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)hello 組態集合中。</span><span class="sxs-lookup"><span data-stu-id="7636b-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="7636b-157">hello 程式碼 hello 連接上使用的資料指標和[cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)方法執行 hello 針對 MySQL 資料庫的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="7636b-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="7636b-158">取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。</span><span class="sxs-lookup"><span data-stu-id="7636b-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="7636b-159">讀取資料</span><span class="sxs-lookup"><span data-stu-id="7636b-159">Read data</span></span>
<span data-ttu-id="7636b-160">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7636b-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="7636b-161">在 hello 程式碼中，會匯入 hello mysql.connector 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7636b-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="7636b-162">hello [connect （)](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html)函式是使用的 tooconnect tooAzure 使用 hello 的 MySQL 資料庫[連接引數](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)hello 組態集合中。</span><span class="sxs-lookup"><span data-stu-id="7636b-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="7636b-163">hello 程式碼 hello 連接上使用的資料指標和[cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)方法執行 hello 針對 MySQL 資料庫的 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7636b-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="7636b-164">hello 資料列會讀取使用 hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html)方法。</span><span class="sxs-lookup"><span data-stu-id="7636b-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="7636b-165">hello 結果集就會保留在集合的資料列和迭代器是使用的 tooloop hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="7636b-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="7636b-166">取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。</span><span class="sxs-lookup"><span data-stu-id="7636b-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="7636b-167">更新資料</span><span class="sxs-lookup"><span data-stu-id="7636b-167">Update data</span></span>
<span data-ttu-id="7636b-168">使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7636b-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="7636b-169">在 hello 程式碼中，會匯入 hello mysql.connector 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7636b-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="7636b-170">hello [connect （)](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html)函式是使用的 tooconnect tooAzure 使用 hello 的 MySQL 資料庫[連接引數](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)hello 組態集合中。</span><span class="sxs-lookup"><span data-stu-id="7636b-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="7636b-171">hello 程式碼 hello 連接上使用的資料指標和[cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)方法執行 hello 針對 MySQL 資料庫的 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7636b-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="7636b-172">取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。</span><span class="sxs-lookup"><span data-stu-id="7636b-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="7636b-173">刪除資料</span><span class="sxs-lookup"><span data-stu-id="7636b-173">Delete data</span></span>
<span data-ttu-id="7636b-174">使用 hello 下列程式碼 tooconnect 並移除資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7636b-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="7636b-175">在 hello 程式碼中，會匯入 hello mysql.connector 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7636b-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="7636b-176">hello [connect （)](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html)函式是使用的 tooconnect tooAzure 使用 hello 的 MySQL 資料庫[連接引數](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)hello 組態集合中。</span><span class="sxs-lookup"><span data-stu-id="7636b-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="7636b-177">hello 程式碼 hello 連接上使用的資料指標和[cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)方法執行 hello 針對 MySQL 資料庫的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="7636b-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="7636b-178">取代 hello `host`， `user`， `password`，和`database`具有 hello 值，指定當您建立 hello 伺服器和資料庫的參數。</span><span class="sxs-lookup"><span data-stu-id="7636b-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7636b-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7636b-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7636b-180">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="7636b-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
