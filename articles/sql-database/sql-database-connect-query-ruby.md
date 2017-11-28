---
title: "Azure SQL Database 的拼音 tooquery aaaUse |Microsoft 文件"
description: "本主題說明如何 toouse 拼音 toocreate 連接 tooan Azure SQL Database 和查詢使用 TRANSACT-SQL 陳述式的程式。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="ff7e5-103">使用拼音 tooquery Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="ff7e5-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="ff7e5-104">本快速入門教學課程示範如何 toouse [Ruby](https://www.ruby-lang.org) toocreate 程式 tooconnect tooan Azure SQL 資料庫，將 TRANSACT-SQL 陳述式 tooquery 資料。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff7e5-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff7e5-105">Prerequisites</span></span>

<span data-ttu-id="ff7e5-106">toocomplete 此快速入門教學課程，請確定您擁有 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="ff7e5-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="ff7e5-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-107">An Azure SQL database.</span></span> <span data-ttu-id="ff7e5-108">本快速入門會使用 hello 資源建立在其中一個這些快速入門：</span><span class="sxs-lookup"><span data-stu-id="ff7e5-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="ff7e5-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="ff7e5-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="ff7e5-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="ff7e5-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="ff7e5-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff7e5-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="ff7e5-112">A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="ff7e5-113">您已安裝適用於您作業系統的 Ruby 和相關軟體。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="ff7e5-114">**MacOS**：安裝 Homebrew、安裝 rbenv 和 ruby-build、安裝 Ruby，然後安裝 FreeTDS。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="ff7e5-115">請參閱[步驟 1.2、1.3、1.4 和 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/)。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="ff7e5-116">**Ubuntu**：安裝 Ruby 的必要條件、安裝 rbenv 和 ruby-build、安裝 Ruby，然後安裝 FreeTDS。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="ff7e5-117">請參閱[步驟 1.2、1.3、1.4 和 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="ff7e5-118">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="ff7e5-118">SQL server connection information</span></span>

<span data-ttu-id="ff7e5-119">收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="ff7e5-120">您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="ff7e5-121">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ff7e5-122">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="ff7e5-123">在 hello**概觀**為您的資料庫頁面上，檢閱 hello 完整的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="ff7e5-124">您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項，hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="ff7e5-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="ff7e5-126">如果您的 Azure SQL Database 伺服器忘記 hello 登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff7e5-127">防火牆規則必須可供您執行本教學課程中的 hello 電腦的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="ff7e5-128">如果您在不同電腦上或有不同的公用 IP 位址，建立[伺服器層級防火牆規則使用 hello Azure 入口網站](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="ff7e5-129">插入程式碼 tooquery SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="ff7e5-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="ff7e5-130">在您慣用的文字編輯器中，建立新的檔案 **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="ff7e5-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="ff7e5-131">以下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼的 hello 取代 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a><span data-ttu-id="ff7e5-132">執行 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="ff7e5-132">Run hello code</span></span>

1. <span data-ttu-id="ff7e5-133">在 hello 命令提示字元中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff7e5-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="ff7e5-134">請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="ff7e5-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ff7e5-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff7e5-135">Next Steps</span></span>
- [<span data-ttu-id="ff7e5-136">設計您的第一個 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ff7e5-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="ff7e5-137">適用於 TinyTDS 的 GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="ff7e5-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="ff7e5-138">回報或發問有關 TinyTDS 的問題</span><span class="sxs-lookup"><span data-stu-id="ff7e5-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="ff7e5-139">Ruby Drivers for SQL Server</span><span class="sxs-lookup"><span data-stu-id="ff7e5-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
