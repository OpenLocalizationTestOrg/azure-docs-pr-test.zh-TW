---
title: "aaaHow tooDump 和還原 Azure 資料庫中的 PostgreSQL |Microsoft 文件"
description: "描述如何 tooextract PostgreSQL 資料庫到傾印檔案以及還原 hello PostgreSQL 資料庫從一個針對 PostgreSQL pg_dump Azure 資料庫中所建立的保存檔案。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="56221-103">使用傾印和還原來移轉 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="56221-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="56221-104">您可以使用[pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract PostgreSQL 資料庫到傾印檔案和[pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL 資料庫從 pg_dump 所建立的保存檔案。</span><span class="sxs-lookup"><span data-stu-id="56221-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56221-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="56221-105">Prerequisites</span></span>
<span data-ttu-id="56221-106">透過這個方式 tooguide toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="56221-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="56221-107">[PostgreSQL server 的 Azure 資料庫](quickstart-create-server-database-portal.md)tooallow 存取的防火牆規則和其下的資料庫。</span><span class="sxs-lookup"><span data-stu-id="56221-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="56221-108">安裝 [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 和 [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="56221-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="56221-109">請遵循這些步驟 toodump 並還原 PostgreSQL 資料庫：</span><span class="sxs-lookup"><span data-stu-id="56221-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="56221-110">建立傾印檔案使用，其中包含載入 hello 資料 toobe pg_dump</span><span class="sxs-lookup"><span data-stu-id="56221-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="56221-111">tooback 上現有的 PostgreSQL 資料庫內部，或在 VM 中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="56221-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="56221-112">比方說，如果您有本機伺服器和名為 **testdb** 的資料庫</span><span class="sxs-lookup"><span data-stu-id="56221-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="56221-113">還原成 hello 目標 Azure 資料庫使用 pg_restore PostrgeSQL hello 資料</span><span class="sxs-lookup"><span data-stu-id="56221-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="56221-114">一旦您已經建立 hello 目標資料庫，您可以使用 hello pg_restore 命令和 hello-d，-dbname 參數 toorestore hello 資料 hello hello 傾印檔案的目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="56221-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="56221-115">在此範例中，請從 hello 傾印檔案中還原 hello 資料**testdb.dump** hello 資料庫**mypgsqldb**目標伺服器上**mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="56221-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="56221-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56221-116">Next steps</span></span>
- <span data-ttu-id="56221-117">toomigrate PostgreSQL 資料庫使用匯出和匯入，請參閱[移轉 PostgreSQL 資料庫使用匯出和匯入](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="56221-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
