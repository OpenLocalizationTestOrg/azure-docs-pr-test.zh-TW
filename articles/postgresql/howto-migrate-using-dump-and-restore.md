---
title: "如何在適用於 PostgreSQL 的 Azure 資料庫中傾印和還原 | Microsoft Docs"
description: "描述如何在適用於 PostgreSQL 的 Azure 資料庫中，將 PostgreSQL 資料庫擷取到傾印檔案，並從 pg_dump 所建立的封存檔案還原 PostgreSQL 資料庫。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 190373c4980b67e16b58700e4b7e65658545c615
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="7a671-103">使用傾印和還原來移轉 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="7a671-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="7a671-104">您可以使用 [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) 將 PostgreSQL 資料庫擷取到傾印檔案，並使用 [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) 從 pg_dump 所建立的封存檔案還原 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a671-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) to restore the PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a671-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a671-105">Prerequisites</span></span>
<span data-ttu-id="7a671-106">若要逐步執行本作法指南，您需要︰</span><span class="sxs-lookup"><span data-stu-id="7a671-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="7a671-107">[適用於 PostgreSQL 的 Azure 資料庫伺服器](quickstart-create-server-database-portal.md)，而且防火牆規則要允許存取其中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a671-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="7a671-108">安裝 [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 和 [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="7a671-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="7a671-109">請遵循下列步驟來傾印和還原 PostgreSQL 資料庫：</span><span class="sxs-lookup"><span data-stu-id="7a671-109">Follow these steps to dump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="7a671-110">使用 pg_dump 建立傾印檔案，其中包含要載入的資料</span><span class="sxs-lookup"><span data-stu-id="7a671-110">Create a dump file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="7a671-111">若要備份內部部署或 VM 中的現有 PostgreSQL 資料庫，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="7a671-111">To back up an existing PostgreSQL database on-premises or in a VM, run the following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="7a671-112">比方說，如果您有本機伺服器和名為 **testdb** 的資料庫</span><span class="sxs-lookup"><span data-stu-id="7a671-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-the-data-into-the-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="7a671-113">使用 pg_restore 將資料還原至目標「適用於 PostrgeSQL 的 Azure 資料庫」</span><span class="sxs-lookup"><span data-stu-id="7a671-113">Restore the data into the target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="7a671-114">建立目標資料庫後，您可以使用 pg_restore 命令和 -d、--dbname 參數，從傾印檔案將資料還原至目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a671-114">Once you have created the target database, you can use the pg_restore command and the -d, --dbname parameter to restore the data into the target database from the dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="7a671-115">在此範例中，請從傾印檔案 **testdb.dump**，將資料還原至目標伺服器 **mypgserver-20170401.postgres.database.azure.com** 上的資料庫 **mypgsqldb**。</span><span class="sxs-lookup"><span data-stu-id="7a671-115">In this example, restore the data from the dump file **testdb.dump** into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="7a671-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a671-116">Next steps</span></span>
- <span data-ttu-id="7a671-117">若要使用匯出和匯入移轉 PostgreSQL 資料庫，請參閱[使用匯出和匯入移轉 PostgreSQL 資料庫](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="7a671-117">To migrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>