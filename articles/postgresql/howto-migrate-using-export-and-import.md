---
title: "資料庫使用匯入和匯出 Azure Database 中 PostgreSQL aaaMigrate |Microsoft 文件"
description: "描述如何將 PostgreSQL 資料庫擷取到指令碼檔案和 hello 資料匯入檔案中的 hello 目標資料庫。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="ba699-103">使用匯出和匯入來移轉 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="ba699-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="ba699-104">您可以使用[pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract PostgreSQL 資料庫到指令碼檔案和[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello hello 目標資料庫，該檔案的資料。</span><span class="sxs-lookup"><span data-stu-id="ba699-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba699-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="ba699-105">Prerequisites</span></span>
<span data-ttu-id="ba699-106">透過這個方式 tooguide toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="ba699-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="ba699-107">[PostgreSQL server 的 Azure 資料庫](quickstart-create-server-database-portal.md)tooallow 存取的防火牆規則和其下的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ba699-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="ba699-108">安裝 [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="ba699-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="ba699-109">安裝 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="ba699-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="ba699-110">請遵循這些步驟 tooexport 和 PostgreSQL 資料庫匯入。</span><span class="sxs-lookup"><span data-stu-id="ba699-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="ba699-111">建立使用 pg_dump 包含 hello 資料 toobe 載入指令碼檔案</span><span class="sxs-lookup"><span data-stu-id="ba699-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="ba699-112">tooexport 您現有的 PostgreSQL 資料庫在內部部署或在 VM tooa sql 指令碼檔案中，執行下列命令，在現有的環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="ba699-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="ba699-113">比方說，如果您有本機伺服器和名為 **testdb** 的資料庫</span><span class="sxs-lookup"><span data-stu-id="ba699-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="ba699-114">匯入目標 PostrgeSQL 的 Azure 資料庫上的 hello 資料</span><span class="sxs-lookup"><span data-stu-id="ba699-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="ba699-115">您可以使用 hello psql 命令列] 和 [hello-d，-dbname 參數 tooimport hello 資料到 PostrgeSQL 我們建立，並從 hello sql 檔案載入資料的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ba699-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="ba699-116">此範例使用 psql 公用程式和指令碼檔名為**testdb.sql**從上一個步驟 tooimport 資料到 hello 資料庫**mypgsqldb**目標伺服器上**mypgserver 20170401.postgres.database.azure.com**。</span><span class="sxs-lookup"><span data-stu-id="ba699-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="ba699-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba699-117">Next steps</span></span>
- <span data-ttu-id="ba699-118">toomigrate PostgreSQL 資料庫使用傾印和還原，請參閱[移轉 PostgreSQL 資料庫使用傾印和還原](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="ba699-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
