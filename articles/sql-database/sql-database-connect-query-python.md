---
title: "Azure SQL Database 的 aaaUse Python tooquery |Microsoft 文件"
description: "本主題說明如何 toouse Python toocreate 連接 tooan Azure SQL Database 和查詢使用 TRANSACT-SQL 陳述式的程式。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="6aeb0-103">使用 Python tooquery Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="6aeb0-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="6aeb0-104">本快速入門示範如何 toouse [Python](https://python.org) tooconnect tooan Azure SQL 資料庫，將 TRANSACT-SQL 陳述式 tooquery 資料。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6aeb0-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="6aeb0-105">Prerequisites</span></span>

<span data-ttu-id="6aeb0-106">toocomplete 此快速入門教學課程，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="6aeb0-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="6aeb0-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-107">An Azure SQL database.</span></span> <span data-ttu-id="6aeb0-108">本快速入門會使用 hello 資源建立在其中一個這些快速入門：</span><span class="sxs-lookup"><span data-stu-id="6aeb0-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="6aeb0-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="6aeb0-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="6aeb0-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="6aeb0-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="6aeb0-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="6aeb0-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="6aeb0-112">A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="6aeb0-113">您已安裝適用於您作業系統的 Python 和相關軟體。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="6aeb0-114">**MacOS**： 安裝 Homebrew，並將 Python，安裝 hello ODBC 驅動程式和 SQLCMD，，然後再安裝 SQL server 的 hello Python 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="6aeb0-115">請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/)。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="6aeb0-116">**Ubuntu**： 安裝 Python 和其他封裝，然後再安裝 hello Python 驅動程式 SQL Server 所需。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="6aeb0-117">請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="6aeb0-118">**Windows**: hello 的 Python （您現在已設定環境變數） 的最新版本的安裝，安裝 hello ODBC 驅動程式和 SQLCMD，然後再安裝 hello Python 驅動程式適用於 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="6aeb0-119">請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/)。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="6aeb0-120">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="6aeb0-120">SQL server connection information</span></span>

<span data-ttu-id="6aeb0-121">收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="6aeb0-122">您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="6aeb0-123">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6aeb0-124">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="6aeb0-125">在 hello**概觀**頁面為您的資料庫檢閱 hello 完整伺服器名稱 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="6aeb0-126">您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="6aeb0-128">如果忘記您的伺服器登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="6aeb0-129">插入程式碼 tooquery SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="6aeb0-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="6aeb0-130">在您慣用的文字編輯器中，建立新的檔案 **sqltest.py**。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="6aeb0-131">以下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼的 hello 取代 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="6aeb0-132">執行 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="6aeb0-132">Run hello code</span></span>

1. <span data-ttu-id="6aeb0-133">在 hello 命令提示字元中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6aeb0-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="6aeb0-134">請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="6aeb0-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6aeb0-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6aeb0-135">Next steps</span></span>

- [<span data-ttu-id="6aeb0-136">設計您的第一個 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6aeb0-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="6aeb0-137">Microsoft Python Drivers for SQL Server</span><span class="sxs-lookup"><span data-stu-id="6aeb0-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="6aeb0-138">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="6aeb0-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

