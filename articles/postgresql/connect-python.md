---
title: "來自 Python PostgreSQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門提供 Python 程式碼範例，您可以使用 tooconnect 和 PostgreSQL 查詢從 Azure 資料庫的資料。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="8831a-103">Azure PostgreSQL 資料庫： 將 Python tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="8831a-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="8831a-104">本快速入門示範如何 toouse [Python](https://python.org) tooconnect tooan PostgreSQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8831a-105">它也示範 toouse SQL 陳述式 tooquery，插入、 更新和刪除 hello 資料庫中的資料從 macOS、 Ubuntu Linux 和 Windows 平台的方式。</span><span class="sxs-lookup"><span data-stu-id="8831a-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="8831a-106">本文章中的 hello 步驟假設您熟悉開發使用 Python，並使用新 tooworking Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8831a-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="8831a-107">Prerequisites</span></span>
<span data-ttu-id="8831a-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="8831a-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="8831a-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="8831a-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="8831a-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="8831a-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="8831a-111">您也會需要：</span><span class="sxs-lookup"><span data-stu-id="8831a-111">You also need:</span></span>
- <span data-ttu-id="8831a-112">已安裝 [python](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="8831a-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="8831a-113">已安裝 [pip](https://pip.pypa.io/en/stable/installing/) 套件 (如果您使用從 [python.org](https://python.org) 下載的 Python 2 >=2.7.9 或 Python 3 >=3.4 二進位檔，便已安裝 pip)。</span><span class="sxs-lookup"><span data-stu-id="8831a-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="8831a-114">Hello Python 連接程式庫安裝 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8831a-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="8831a-115">安裝 hello [psycopg2](http://initd.org/psycopg/docs/install.html)套件，可讓您 tooconnect 和查詢 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="8831a-116">psycopg2 是[用於 PyPI](https://pypi.python.org/pypi/psycopg2/) hello 形式[滾輪](http://pythonwheels.com/)hello 最常見的平台 (Linux OSX，Windows) 的封裝。</span><span class="sxs-lookup"><span data-stu-id="8831a-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="8831a-117">使用 pip 安裝 tooget hello 二進位版本 hello 模組包含所有 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="8831a-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="8831a-118">在自己的電腦上啟動命令列介面：</span><span class="sxs-lookup"><span data-stu-id="8831a-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="8831a-119">在 Linux 上啟動 hello Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="8831a-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="8831a-120">MacOS 上啟動終端機 hello。</span><span class="sxs-lookup"><span data-stu-id="8831a-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="8831a-121">在 Windows 中，啟動 從 開始 功能表中的 hello hello 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="8831a-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="8831a-122">請確定您執行命令，例如使用 pip hello 最新版本：</span><span class="sxs-lookup"><span data-stu-id="8831a-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="8831a-123">執行下列命令 tooinstall hello psycopg2 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="8831a-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="8831a-124">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="8831a-124">Get connection information</span></span>
<span data-ttu-id="8831a-125">取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8831a-126">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="8831a-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="8831a-127">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="8831a-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8831a-128">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**並搜尋**mypgserver 20170401** （您剛才建立的 hello 伺服器）。</span><span class="sxs-lookup"><span data-stu-id="8831a-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="8831a-129">按一下伺服器名稱，hello **mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="8831a-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="8831a-130">選取 hello 伺服器**概觀**頁面，然後再記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="8831a-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="8831a-131">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="8831a-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="8831a-132">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="8831a-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="8831a-133">如何 toorun Python 程式碼</span><span class="sxs-lookup"><span data-stu-id="8831a-133">How toorun Python code</span></span>
<span data-ttu-id="8831a-134">本主題總共包含四個程式碼範例，各自會執行一項特定功能。</span><span class="sxs-lookup"><span data-stu-id="8831a-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="8831a-135">hello 下列指示表示 toocreate 文字檔案時，如何插入程式碼區塊，然後儲存 hello 檔案，以便稍後執行。</span><span class="sxs-lookup"><span data-stu-id="8831a-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="8831a-136">為確定 toocreate 四個不同的檔案，一個用於每個程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="8831a-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="8831a-137">使用您慣用的文字編輯器，建立新的檔案。</span><span class="sxs-lookup"><span data-stu-id="8831a-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="8831a-138">複製並貼在 hello hello 文字檔案到下列各節中的 hello 程式碼範例的其中一個。</span><span class="sxs-lookup"><span data-stu-id="8831a-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="8831a-139">取代 hello**主機**， **dbname**，**使用者**，和**密碼**具有您指定當您建立 hello hello 值的參數伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="8831a-140">Hello 檔案與儲存 hello.py 擴充功能 (例如 postgres.py) 到您的專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="8831a-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="8831a-141">如果您要執行 hello Windows OS，是確定 tooselect utf-8 編碼方式儲存 hello 檔案時。</span><span class="sxs-lookup"><span data-stu-id="8831a-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="8831a-142">啟動 hello 命令提示字元或 Bash 殼層，然後再變更 hello 目錄 tooyour 專案資料夾，例如`cd postgres`。</span><span class="sxs-lookup"><span data-stu-id="8831a-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="8831a-143">toorun hello 程式碼中，後面接著 hello 檔案名稱，例如 Python 命令的型別 hello `Python postgres.py`。</span><span class="sxs-lookup"><span data-stu-id="8831a-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="8831a-144">從 Python 第 3 版開始，您可能會看見 hello 錯誤`SyntaxError: Missing parentheses in call too'print'`時執行下列程式碼區塊的 hello。</span><span class="sxs-lookup"><span data-stu-id="8831a-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="8831a-145">如果發生這種情況，會取代每個呼叫 toohello 命令`print "string"`函式呼叫使用括號，例如`print("string")`。</span><span class="sxs-lookup"><span data-stu-id="8831a-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="8831a-146">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="8831a-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="8831a-147">使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用[psycopg2.connect](http://initd.org/psycopg/docs/connection.html)函式與**插入**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8831a-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="8831a-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute)函式是針對 PostgreSQL 資料庫使用的 tooexecute hello SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="8831a-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="8831a-149">Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

<span data-ttu-id="8831a-150">Hello 之後執行程式碼成功，hello 輸出會出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8831a-150">After hello code runs successfully, hello output appears as follows:</span></span>

![命令列輸出](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="8831a-152">讀取資料</span><span class="sxs-lookup"><span data-stu-id="8831a-152">Read data</span></span>
<span data-ttu-id="8831a-153">使用 hello 下列程式碼插入使用 tooread hello 資料[cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute)函式與**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8831a-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="8831a-154">此函式接受查詢並傳回結果集，可以反覆使用 hello [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall)。</span><span class="sxs-lookup"><span data-stu-id="8831a-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="8831a-155">Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a><span data-ttu-id="8831a-156">更新資料</span><span class="sxs-lookup"><span data-stu-id="8831a-156">Update data</span></span>
<span data-ttu-id="8831a-157">使用 hello 下列程式碼 tooupdate hello 清查的資料列之前插入使用[cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute)函式與**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8831a-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="8831a-158">Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="8831a-159">刪除資料</span><span class="sxs-lookup"><span data-stu-id="8831a-159">Delete data</span></span>
<span data-ttu-id="8831a-160">使用 hello 下列程式碼之前插入使用中的清查項目 toodelete [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute)函式與**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8831a-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="8831a-161">Hello 主機、 dbname、 使用者和密碼參數取代 hello 值，指定當您建立 hello 伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="8831a-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="8831a-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8831a-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8831a-163">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="8831a-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
