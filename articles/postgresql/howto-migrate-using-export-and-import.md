---
title: "在適用於 PostgreSQL 的 Azure 資料庫中使用匯入和匯出移轉資料庫 | Microsoft Docs"
description: "描述如何將 PostgreSQL 資料庫擷取到指令碼檔案，並從該檔案將資料匯入目標資料庫。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5e306d516d04789e4526bfd09bf99139b83573ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="4f68c-103">使用匯出和匯入來移轉 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="4f68c-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="4f68c-104">您可以使用 [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) 將 PostgreSQL 資料庫擷取到指令碼檔案，並使用 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 從該檔案將資料匯入目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="4f68c-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to import the data into the target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f68c-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="4f68c-105">Prerequisites</span></span>
<span data-ttu-id="4f68c-106">若要逐步執行本作法指南，您需要︰</span><span class="sxs-lookup"><span data-stu-id="4f68c-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="4f68c-107">[適用於 PostgreSQL 的 Azure 資料庫伺服器](quickstart-create-server-database-portal.md)，而且防火牆規則要允許存取其中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4f68c-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="4f68c-108">安裝 [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="4f68c-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="4f68c-109">安裝 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="4f68c-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="4f68c-110">請遵循下列步驟來匯出和匯入 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4f68c-110">Follow these steps to export and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="4f68c-111">使用 pg_dump 建立指令碼檔案，其中包含要載入的資料</span><span class="sxs-lookup"><span data-stu-id="4f68c-111">Create a script file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="4f68c-112">若要將內部部署或 VM 中的現有 PostgreSQL 資料庫匯出至 sql 指令碼檔，請在您現有的環境中執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="4f68c-112">To export your existing PostgreSQL database on-premises or in a VM to a sql script file, run the following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="4f68c-113">比方說，如果您有本機伺服器和名為 **testdb** 的資料庫</span><span class="sxs-lookup"><span data-stu-id="4f68c-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="4f68c-114">在目標「適用於 PostrgeSQL 的 Azure 資料庫」上匯入資料</span><span class="sxs-lookup"><span data-stu-id="4f68c-114">Import the data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="4f68c-115">您可以使用 psql 命令列和 -d, --dbname 參數，將資料匯入我們建立之適用於 PostrgeSQL 的 Azure 資料庫，並從 sql 檔案載入資料。</span><span class="sxs-lookup"><span data-stu-id="4f68c-115">You can use the psql command line and the -d, --dbname parameter to import the data into Azure Database for PostrgeSQL we created and load data from the sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="4f68c-116">此範例使用 psql 公用程式和上一個步驟中名為 **testdb.sql** 的指令碼檔案，將資料匯入目標伺服器 **mypgserver-20170401.postgres.database.azure.com** 上的資料庫 **mypgsqldb**。</span><span class="sxs-lookup"><span data-stu-id="4f68c-116">This example uses psql utility and a script file named **testdb.sql** from previous step to import data into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="4f68c-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f68c-117">Next steps</span></span>
- <span data-ttu-id="4f68c-118">若要使用傾印和還原移轉 PostgreSQL 資料庫，請參閱[使用傾印和還原來移轉 PostgreSQL 資料庫](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="4f68c-118">To migrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>