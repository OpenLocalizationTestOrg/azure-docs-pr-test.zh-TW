---
title: "Azure PostgreSQL 資料庫中的 aaaUsing PostgreSQL 延伸 |Microsoft 文件"
description: "描述 hello Azure Database 中使用擴充功能，如 PostgreSQL 資料庫的能力 tooextend hello 功能。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a><span data-ttu-id="43b05-103">適用於 PostgreSQL 的 Azure 資料庫中的 PostgreSQL 擴充功能</span><span class="sxs-lookup"><span data-stu-id="43b05-103">PostgreSQL Extensions in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="43b05-104">PostgreSQL 提供 hello 資料庫使用擴充功能的能力 tooextend hello 功能。</span><span class="sxs-lookup"><span data-stu-id="43b05-104">PostgreSQL provides hello ability tooextend hello functionality of your database using extensions.</span></span> <span data-ttu-id="43b05-105">擴充功能允許多個相關的 SQL 物件 toobe 單一封裝中配套在一起，可載入或從您的資料庫，使用單一命令中移除。</span><span class="sxs-lookup"><span data-stu-id="43b05-105">Extensions allow for multiple related SQL objects toobe bundled together in a single package and can be loaded or removed from your database with a single command.</span></span> <span data-ttu-id="43b05-106">一次載入 hello 資料庫的擴充功能可以運作一樣內建的功能。</span><span class="sxs-lookup"><span data-stu-id="43b05-106">Extensions once loaded into hello database can function just like features that are built in.</span></span> <span data-ttu-id="43b05-107">如需 PostgreSQL 擴充功能的詳細資訊，請參閱[將相關物件封裝成擴充功能 (英文)](https://www.postgresql.org/docs/9.6/static/extend-extensions.html)。</span><span class="sxs-lookup"><span data-stu-id="43b05-107">For more information on PostgreSQL extensions, see [Packaging Related Objects into an Extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).</span></span>

## <a name="how-toouse-postgresql-extensions"></a><span data-ttu-id="43b05-108">如何 toouse PostgreSQL 延伸模組嗎？</span><span class="sxs-lookup"><span data-stu-id="43b05-108">How toouse PostgreSQL extensions?</span></span>
<span data-ttu-id="43b05-109">PostgreSQL 延伸模組需要 toobe 安裝您的資料庫，才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="43b05-109">PostgreSQL extensions need toobe installed for your database before you can use them.</span></span> <span data-ttu-id="43b05-110">執行 tooinstall 特定的副檔名為[建立副檔名](https://www.postgresql.org/docs/9.6/static/sql-createextension.html)命令從 psql 工具 tooload hello 封裝的物件至您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="43b05-110">tooinstall a particular extension, run the [CREATE EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) command from psql tool tooload hello packaged objects into your database.</span></span>

<span data-ttu-id="43b05-111">適用於 PostgreSQL 的 Azure 資料庫支援的部分重要擴充功能如此處所列。</span><span class="sxs-lookup"><span data-stu-id="43b05-111">Azure Database for PostgreSQL supports a subset of key extensions as listed here.</span></span> <span data-ttu-id="43b05-112">超出 hello 列示，不支援其他擴充功能。</span><span class="sxs-lookup"><span data-stu-id="43b05-112">Beyond hello ones listed, other extensions are not supported.</span></span> <span data-ttu-id="43b05-113">您無法針對適用於 PostgreSQL 的 Azure 資料庫服務，自行建立擴充功能。</span><span class="sxs-lookup"><span data-stu-id="43b05-113">You cannot create your own extension with Azure Database for PostgreSQL service.</span></span>

## <a name="extensions-supported-by-azure-database-for-postgresql"></a><span data-ttu-id="43b05-114">適用於 PostgreSQL 的 Azure 資料庫支援的擴充功能</span><span class="sxs-lookup"><span data-stu-id="43b05-114">Extensions supported by Azure Database for PostgreSQL</span></span>
<span data-ttu-id="43b05-115">hello 以下表格列出 hello 標準 PostgreSQL 擴充功能會針對 PostgreSQL 目前支援的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="43b05-115">hello following tables list hello standard PostgreSQL extensions that are currently supported by Azure Database for PostgreSQL.</span></span> <span data-ttu-id="43b05-116">您也可以藉由查詢 pg\_available\_extensions 來取得此資訊。</span><span class="sxs-lookup"><span data-stu-id="43b05-116">You can also obtain this information by querying pg\_available\_extensions.</span></span> 

### <a name="data-types-extensions"></a><span data-ttu-id="43b05-117">資料類型擴充功能</span><span class="sxs-lookup"><span data-stu-id="43b05-117">Data types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="43b05-118">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="43b05-118">**Extension**</span></span> | <span data-ttu-id="43b05-119">**說明**</span><span class="sxs-lookup"><span data-stu-id="43b05-119">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="43b05-120">citext</span><span class="sxs-lookup"><span data-stu-id="43b05-120">citext</span></span>](https://www.postgresql.org/docs/9.6/static/citext.html) | <span data-ttu-id="43b05-121">提供不區分大小寫的字元字串類型</span><span class="sxs-lookup"><span data-stu-id="43b05-121">Provides a case-insensitive character string type</span></span> |
| [<span data-ttu-id="43b05-122">hstore</span><span class="sxs-lookup"><span data-stu-id="43b05-122">hstore</span></span>](https://www.postgresql.org/docs/9.6/static/hstore.html) | <span data-ttu-id="43b05-123">提供用來儲存索引鍵/值組之集合的資料類型</span><span class="sxs-lookup"><span data-stu-id="43b05-123">Provides data type for storing sets of key/value pairs</span></span> |

### <a name="functions-extensions"></a><span data-ttu-id="43b05-124">函數擴充功能</span><span class="sxs-lookup"><span data-stu-id="43b05-124">Functions extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="43b05-125">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="43b05-125">**Extension**</span></span> | <span data-ttu-id="43b05-126">**說明**</span><span class="sxs-lookup"><span data-stu-id="43b05-126">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="43b05-127">fuzzystrmatch</span><span class="sxs-lookup"><span data-stu-id="43b05-127">fuzzystrmatch</span></span>](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | <span data-ttu-id="43b05-128">提供數個函式 toodetermine 相似與字串之間的距離。</span><span class="sxs-lookup"><span data-stu-id="43b05-128">Provides several functions toodetermine similarities and distance between strings.</span></span> |
| [<span data-ttu-id="43b05-129">intarray</span><span class="sxs-lookup"><span data-stu-id="43b05-129">intarray</span></span>](https://www.postgresql.org/docs/9.6/static/intarray.html) | <span data-ttu-id="43b05-130">提供函數和運算子來操作無 null 的整數陣列。</span><span class="sxs-lookup"><span data-stu-id="43b05-130">Provides functions and operators for manipulating null-free arrays of integers.</span></span> |
| [<span data-ttu-id="43b05-131">pgcrypto</span><span class="sxs-lookup"><span data-stu-id="43b05-131">pgcrypto</span></span>](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | <span data-ttu-id="43b05-132">提供密碼編譯函數</span><span class="sxs-lookup"><span data-stu-id="43b05-132">Provides cryptographic functions</span></span> |
| [<span data-ttu-id="43b05-133">pg\_partman</span><span class="sxs-lookup"><span data-stu-id="43b05-133">pg\_partman</span></span>](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | <span data-ttu-id="43b05-134">依時間或識別碼來管理資料分割資料表</span><span class="sxs-lookup"><span data-stu-id="43b05-134">Manages partitioned tables by time or ID</span></span> |
| [<span data-ttu-id="43b05-135">pg\_trgm</span><span class="sxs-lookup"><span data-stu-id="43b05-135">pg\_trgm</span></span>](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | <span data-ttu-id="43b05-136">提供判斷 hello 根據三字母組比對英數字元的文字相似度的函數和運算子</span><span class="sxs-lookup"><span data-stu-id="43b05-136">Provides functions and operators for determining hello similarity of alphanumeric text based on trigram matching</span></span> |
| [<span data-ttu-id="43b05-137">uuid-ossp</span><span class="sxs-lookup"><span data-stu-id="43b05-137">uuid-ossp</span></span>](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | <span data-ttu-id="43b05-138">產生通用唯一識別碼 (UUID)</span><span class="sxs-lookup"><span data-stu-id="43b05-138">Generate universally unique identifiers (UUIDs)</span></span> |

### <a name="full-text-search-extensions"></a><span data-ttu-id="43b05-139">全文檢索搜尋擴充功能</span><span class="sxs-lookup"><span data-stu-id="43b05-139">Full-text Search extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="43b05-140">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="43b05-140">**Extension**</span></span> | <span data-ttu-id="43b05-141">**說明**</span><span class="sxs-lookup"><span data-stu-id="43b05-141">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="43b05-142">unaccent</span><span class="sxs-lookup"><span data-stu-id="43b05-142">unaccent</span></span>](https://www.postgresql.org/docs/9.6/static/unaccent.html) | <span data-ttu-id="43b05-143">文字搜尋字典，可從詞彙中移除重音符號 (變音符號)。</span><span class="sxs-lookup"><span data-stu-id="43b05-143">A text search dictionary that removes accents (diacritic signs) from lexemes.</span></span> |

### <a name="index-types-extensions"></a><span data-ttu-id="43b05-144">索引類型擴充功能</span><span class="sxs-lookup"><span data-stu-id="43b05-144">Index Types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="43b05-145">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="43b05-145">**Extension**</span></span> | <span data-ttu-id="43b05-146">**說明**</span><span class="sxs-lookup"><span data-stu-id="43b05-146">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="43b05-147">btree\_gin</span><span class="sxs-lookup"><span data-stu-id="43b05-147">btree\_gin</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | <span data-ttu-id="43b05-148">提供範例 GIN 運算子類別，可針對特定資料類型實作類似 B 型樹狀結構的行為。</span><span class="sxs-lookup"><span data-stu-id="43b05-148">Provides sample GIN operator classes that implement B-tree like behavior for certain data types.</span></span> |
| [<span data-ttu-id="43b05-149">btree\_gist</span><span class="sxs-lookup"><span data-stu-id="43b05-149">btree\_gist</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | <span data-ttu-id="43b05-150">提供可實作 B 型樹狀結構的 GiST 索引運算子類別。</span><span class="sxs-lookup"><span data-stu-id="43b05-150">Provides GiST index operator classes that implement B-tree.</span></span> |

### <a name="language-extensions"></a><span data-ttu-id="43b05-151">語言擴充功能</span><span class="sxs-lookup"><span data-stu-id="43b05-151">Language extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="43b05-152">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="43b05-152">**Extension**</span></span> | <span data-ttu-id="43b05-153">**說明**</span><span class="sxs-lookup"><span data-stu-id="43b05-153">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="43b05-154">plpgsql</span><span class="sxs-lookup"><span data-stu-id="43b05-154">plpgsql</span></span>](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | <span data-ttu-id="43b05-155">PL/pgSQL 可載入的程序性語言</span><span class="sxs-lookup"><span data-stu-id="43b05-155">PL/pgSQL loadable procedural language</span></span> |

### <a name="miscellaneous-extensions"></a><span data-ttu-id="43b05-156">其他擴充功能</span><span class="sxs-lookup"><span data-stu-id="43b05-156">Miscellaneous extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="43b05-157">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="43b05-157">**Extension**</span></span> | <span data-ttu-id="43b05-158">**說明**</span><span class="sxs-lookup"><span data-stu-id="43b05-158">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="43b05-159">pg\_buffercache</span><span class="sxs-lookup"><span data-stu-id="43b05-159">pg\_buffercache</span></span>](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | <span data-ttu-id="43b05-160">提供方法來檢查即時 hello 共用緩衝區快取中的情況。</span><span class="sxs-lookup"><span data-stu-id="43b05-160">Provides a means for examining what's happening in hello shared buffer cache in real time.</span></span> |
| [<span data-ttu-id="43b05-161">pg\_prewarm</span><span class="sxs-lookup"><span data-stu-id="43b05-161">pg\_prewarm</span></span>](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | <span data-ttu-id="43b05-162">會提供資料的方式 tooload 關聯至 hello 緩衝快取。</span><span class="sxs-lookup"><span data-stu-id="43b05-162">Provides a way tooload relation data into hello buffer cache.</span></span> |
| [<span data-ttu-id="43b05-163">pg\_stat\_statements</span><span class="sxs-lookup"><span data-stu-id="43b05-163">pg\_stat\_statements</span></span>](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | <span data-ttu-id="43b05-164">提供一種方法，來追蹤伺服器所執行之所有 SQL 陳述式的執行統計資料。</span><span class="sxs-lookup"><span data-stu-id="43b05-164">Provides a means for tracking execution statistics of all SQL statements executed by a server.</span></span> |
| [<span data-ttu-id="43b05-165">postgres\_fdw</span><span class="sxs-lookup"><span data-stu-id="43b05-165">postgres\_fdw</span></span>](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | <span data-ttu-id="43b05-166">使用 tooaccess 資料儲存在外部 PostgreSQL 伺服器中的外部資料包裝函式</span><span class="sxs-lookup"><span data-stu-id="43b05-166">Foreign-data wrapper used tooaccess data stored in external PostgreSQL servers</span></span> |

### <a name="postgis"></a><span data-ttu-id="43b05-167">PostGIS</span><span class="sxs-lookup"><span data-stu-id="43b05-167">PostGIS</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="43b05-168">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="43b05-168">**Extension**</span></span> | <span data-ttu-id="43b05-169">**說明**</span><span class="sxs-lookup"><span data-stu-id="43b05-169">**Description**</span></span> |
|---|---|
| <span data-ttu-id="43b05-170">[PostGIS](http://www.postgis.net/)、postgis\_topology、postgis\_tiger\_geocoder、postgis\_sfcgal</span><span class="sxs-lookup"><span data-stu-id="43b05-170">[PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal</span></span> | <span data-ttu-id="43b05-171">適用於 PostgreSQL 的空間與地理物件。</span><span class="sxs-lookup"><span data-stu-id="43b05-171">Spatial and geographic objects for PostgreSQL.</span></span> |
| <span data-ttu-id="43b05-172">address\_standardizer、address\_standardizer\_data\_us</span><span class="sxs-lookup"><span data-stu-id="43b05-172">address\_standardizer, address\_standardizer\_data\_us</span></span> | <span data-ttu-id="43b05-173">使用的 tooparse 組成項目位址。</span><span class="sxs-lookup"><span data-stu-id="43b05-173">Used tooparse an address into constituent elements.</span></span> <span data-ttu-id="43b05-174">使用 toosupport 地理編碼位址正規化步驟。</span><span class="sxs-lookup"><span data-stu-id="43b05-174">Used toosupport geocoding address normalization step.</span></span> |
| [<span data-ttu-id="43b05-175">pgrouting</span><span class="sxs-lookup"><span data-stu-id="43b05-175">pgrouting</span></span>](http://pgrouting.org/) | <span data-ttu-id="43b05-176">擴充 hello PostGIS / PostgreSQL geospatial 資料庫 tooprovide geospatial 路由功能。</span><span class="sxs-lookup"><span data-stu-id="43b05-176">Extends hello PostGIS / PostgreSQL geospatial database tooprovide geospatial routing functionality.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43b05-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43b05-177">Next steps</span></span>
<span data-ttu-id="43b05-178">沒看見您想要 toouse 擴充功能嗎？</span><span class="sxs-lookup"><span data-stu-id="43b05-178">Don't see an extension you'd like toouse?</span></span> <span data-ttu-id="43b05-179">請告訴我們。</span><span class="sxs-lookup"><span data-stu-id="43b05-179">Please let us know.</span></span> <span data-ttu-id="43b05-180">在我們的[客戶意見反應論壇 (英文)](https://feedback.azure.com/forums/597976-azure-database-for-postgresql) 中投票給現有的要求，或建立新的意見反應和期望。</span><span class="sxs-lookup"><span data-stu-id="43b05-180">Vote for existing requests or create new feedback and wishes in our [Customer feedback forum](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).</span></span>
