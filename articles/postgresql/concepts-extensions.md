---
title: "在適用於 PostgreSQL 的 Azure 資料庫中使用 PostgreSQL 擴充功能 | Microsoft Docs"
description: "描述下列功能：在適用於 PostgreSQL 的 Azure 資料庫中，使用擴充功能來擴充資料庫功能。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: 755d1cf1a921f6be8f28a4a8ae515db08d904fcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a><span data-ttu-id="7ec31-103">適用於 PostgreSQL 的 Azure 資料庫中的 PostgreSQL 擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ec31-103">PostgreSQL Extensions in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="7ec31-104">PostgreSQL 提供下列功能：使用擴充功能來擴充您的資料庫功能。</span><span class="sxs-lookup"><span data-stu-id="7ec31-104">PostgreSQL provides the ability to extend the functionality of your database using extensions.</span></span> <span data-ttu-id="7ec31-105">擴充功能可在單一封裝中搭配使用多個相關的 SQL 物件，並可使用單一命令從您的資料庫加以載入或移除。</span><span class="sxs-lookup"><span data-stu-id="7ec31-105">Extensions allow for multiple related SQL objects to be bundled together in a single package and can be loaded or removed from your database with a single command.</span></span> <span data-ttu-id="7ec31-106">載入資料庫後的擴充功能運作方式就像內建功能一樣。</span><span class="sxs-lookup"><span data-stu-id="7ec31-106">Extensions once loaded into the database can function just like features that are built in.</span></span> <span data-ttu-id="7ec31-107">如需 PostgreSQL 擴充功能的詳細資訊，請參閱[將相關物件封裝成擴充功能 (英文)](https://www.postgresql.org/docs/9.6/static/extend-extensions.html)。</span><span class="sxs-lookup"><span data-stu-id="7ec31-107">For more information on PostgreSQL extensions, see [Packaging Related Objects into an Extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).</span></span>

## <a name="how-to-use-postgresql-extensions"></a><span data-ttu-id="7ec31-108">如何使用 PostgreSQL 擴充功能？</span><span class="sxs-lookup"><span data-stu-id="7ec31-108">How to use PostgreSQL extensions?</span></span>
<span data-ttu-id="7ec31-109">您必須先針對資料庫安裝 PostgreSQL 擴充功能，然後才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="7ec31-109">PostgreSQL extensions need to be installed for your database before you can use them.</span></span> <span data-ttu-id="7ec31-110">若要安裝特定的擴充功能，請從 psql 工具執行 [CREATE EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) 命令，以將封裝的物件載入至您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7ec31-110">To install a particular extension, run the [CREATE EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) command from psql tool to load the packaged objects into your database.</span></span>

<span data-ttu-id="7ec31-111">適用於 PostgreSQL 的 Azure 資料庫支援的部分重要擴充功能如此處所列。</span><span class="sxs-lookup"><span data-stu-id="7ec31-111">Azure Database for PostgreSQL supports a subset of key extensions as listed here.</span></span> <span data-ttu-id="7ec31-112">不支援此處列出之外的其他擴充功能。</span><span class="sxs-lookup"><span data-stu-id="7ec31-112">Beyond the ones listed, other extensions are not supported.</span></span> <span data-ttu-id="7ec31-113">您無法針對適用於 PostgreSQL 的 Azure 資料庫服務，自行建立擴充功能。</span><span class="sxs-lookup"><span data-stu-id="7ec31-113">You cannot create your own extension with Azure Database for PostgreSQL service.</span></span>

## <a name="extensions-supported-by-azure-database-for-postgresql"></a><span data-ttu-id="7ec31-114">適用於 PostgreSQL 的 Azure 資料庫支援的擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ec31-114">Extensions supported by Azure Database for PostgreSQL</span></span>
<span data-ttu-id="7ec31-115">下表列出適用於 PostgreSQL 的 Azure 資料庫目前支援的標準 PostgreSQL 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="7ec31-115">The following tables list the standard PostgreSQL extensions that are currently supported by Azure Database for PostgreSQL.</span></span> <span data-ttu-id="7ec31-116">您也可以藉由查詢 pg\_available\_extensions 來取得此資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec31-116">You can also obtain this information by querying pg\_available\_extensions.</span></span> 

### <a name="data-types-extensions"></a><span data-ttu-id="7ec31-117">資料類型擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ec31-117">Data types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="7ec31-118">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="7ec31-118">**Extension**</span></span> | <span data-ttu-id="7ec31-119">**說明**</span><span class="sxs-lookup"><span data-stu-id="7ec31-119">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="7ec31-120">citext</span><span class="sxs-lookup"><span data-stu-id="7ec31-120">citext</span></span>](https://www.postgresql.org/docs/9.6/static/citext.html) | <span data-ttu-id="7ec31-121">提供不區分大小寫的字元字串類型</span><span class="sxs-lookup"><span data-stu-id="7ec31-121">Provides a case-insensitive character string type</span></span> |
| [<span data-ttu-id="7ec31-122">hstore</span><span class="sxs-lookup"><span data-stu-id="7ec31-122">hstore</span></span>](https://www.postgresql.org/docs/9.6/static/hstore.html) | <span data-ttu-id="7ec31-123">提供用來儲存索引鍵/值組之集合的資料類型</span><span class="sxs-lookup"><span data-stu-id="7ec31-123">Provides data type for storing sets of key/value pairs</span></span> |

### <a name="functions-extensions"></a><span data-ttu-id="7ec31-124">函數擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ec31-124">Functions extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="7ec31-125">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="7ec31-125">**Extension**</span></span> | <span data-ttu-id="7ec31-126">**說明**</span><span class="sxs-lookup"><span data-stu-id="7ec31-126">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="7ec31-127">fuzzystrmatch</span><span class="sxs-lookup"><span data-stu-id="7ec31-127">fuzzystrmatch</span></span>](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | <span data-ttu-id="7ec31-128">提供數個函數來判斷字串之間的相似性與距離。</span><span class="sxs-lookup"><span data-stu-id="7ec31-128">Provides several functions to determine similarities and distance between strings.</span></span> |
| [<span data-ttu-id="7ec31-129">intarray</span><span class="sxs-lookup"><span data-stu-id="7ec31-129">intarray</span></span>](https://www.postgresql.org/docs/9.6/static/intarray.html) | <span data-ttu-id="7ec31-130">提供函數和運算子來操作無 null 的整數陣列。</span><span class="sxs-lookup"><span data-stu-id="7ec31-130">Provides functions and operators for manipulating null-free arrays of integers.</span></span> |
| [<span data-ttu-id="7ec31-131">pgcrypto</span><span class="sxs-lookup"><span data-stu-id="7ec31-131">pgcrypto</span></span>](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | <span data-ttu-id="7ec31-132">提供密碼編譯函數</span><span class="sxs-lookup"><span data-stu-id="7ec31-132">Provides cryptographic functions</span></span> |
| [<span data-ttu-id="7ec31-133">pg\_partman</span><span class="sxs-lookup"><span data-stu-id="7ec31-133">pg\_partman</span></span>](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | <span data-ttu-id="7ec31-134">依時間或識別碼來管理資料分割資料表</span><span class="sxs-lookup"><span data-stu-id="7ec31-134">Manages partitioned tables by time or ID</span></span> |
| [<span data-ttu-id="7ec31-135">pg\_trgm</span><span class="sxs-lookup"><span data-stu-id="7ec31-135">pg\_trgm</span></span>](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | <span data-ttu-id="7ec31-136">提供可根據三併詞比對判斷英數文字相似度的函數和運算子</span><span class="sxs-lookup"><span data-stu-id="7ec31-136">Provides functions and operators for determining the similarity of alphanumeric text based on trigram matching</span></span> |
| [<span data-ttu-id="7ec31-137">uuid-ossp</span><span class="sxs-lookup"><span data-stu-id="7ec31-137">uuid-ossp</span></span>](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | <span data-ttu-id="7ec31-138">產生通用唯一識別碼 (UUID)</span><span class="sxs-lookup"><span data-stu-id="7ec31-138">Generate universally unique identifiers (UUIDs)</span></span> |

### <a name="full-text-search-extensions"></a><span data-ttu-id="7ec31-139">全文檢索搜尋擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ec31-139">Full-text Search extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="7ec31-140">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="7ec31-140">**Extension**</span></span> | <span data-ttu-id="7ec31-141">**說明**</span><span class="sxs-lookup"><span data-stu-id="7ec31-141">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="7ec31-142">unaccent</span><span class="sxs-lookup"><span data-stu-id="7ec31-142">unaccent</span></span>](https://www.postgresql.org/docs/9.6/static/unaccent.html) | <span data-ttu-id="7ec31-143">文字搜尋字典，可從詞彙中移除重音符號 (變音符號)。</span><span class="sxs-lookup"><span data-stu-id="7ec31-143">A text search dictionary that removes accents (diacritic signs) from lexemes.</span></span> |

### <a name="index-types-extensions"></a><span data-ttu-id="7ec31-144">索引類型擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ec31-144">Index Types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="7ec31-145">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="7ec31-145">**Extension**</span></span> | <span data-ttu-id="7ec31-146">**說明**</span><span class="sxs-lookup"><span data-stu-id="7ec31-146">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="7ec31-147">btree\_gin</span><span class="sxs-lookup"><span data-stu-id="7ec31-147">btree\_gin</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | <span data-ttu-id="7ec31-148">提供範例 GIN 運算子類別，可針對特定資料類型實作類似 B 型樹狀結構的行為。</span><span class="sxs-lookup"><span data-stu-id="7ec31-148">Provides sample GIN operator classes that implement B-tree like behavior for certain data types.</span></span> |
| [<span data-ttu-id="7ec31-149">btree\_gist</span><span class="sxs-lookup"><span data-stu-id="7ec31-149">btree\_gist</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | <span data-ttu-id="7ec31-150">提供可實作 B 型樹狀結構的 GiST 索引運算子類別。</span><span class="sxs-lookup"><span data-stu-id="7ec31-150">Provides GiST index operator classes that implement B-tree.</span></span> |

### <a name="language-extensions"></a><span data-ttu-id="7ec31-151">語言擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ec31-151">Language extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="7ec31-152">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="7ec31-152">**Extension**</span></span> | <span data-ttu-id="7ec31-153">**說明**</span><span class="sxs-lookup"><span data-stu-id="7ec31-153">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="7ec31-154">plpgsql</span><span class="sxs-lookup"><span data-stu-id="7ec31-154">plpgsql</span></span>](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | <span data-ttu-id="7ec31-155">PL/pgSQL 可載入的程序性語言</span><span class="sxs-lookup"><span data-stu-id="7ec31-155">PL/pgSQL loadable procedural language</span></span> |

### <a name="miscellaneous-extensions"></a><span data-ttu-id="7ec31-156">其他擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ec31-156">Miscellaneous extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="7ec31-157">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="7ec31-157">**Extension**</span></span> | <span data-ttu-id="7ec31-158">**說明**</span><span class="sxs-lookup"><span data-stu-id="7ec31-158">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="7ec31-159">pg\_buffercache</span><span class="sxs-lookup"><span data-stu-id="7ec31-159">pg\_buffercache</span></span>](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | <span data-ttu-id="7ec31-160">提供一種方法，即時檢查共用緩衝區快取中發生的狀況。</span><span class="sxs-lookup"><span data-stu-id="7ec31-160">Provides a means for examining what's happening in the shared buffer cache in real time.</span></span> |
| [<span data-ttu-id="7ec31-161">pg\_prewarm</span><span class="sxs-lookup"><span data-stu-id="7ec31-161">pg\_prewarm</span></span>](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | <span data-ttu-id="7ec31-162">提供一種方式，來將關聯資料載入至緩衝區快取。</span><span class="sxs-lookup"><span data-stu-id="7ec31-162">Provides a way to load relation data into the buffer cache.</span></span> |
| [<span data-ttu-id="7ec31-163">pg\_stat\_statements</span><span class="sxs-lookup"><span data-stu-id="7ec31-163">pg\_stat\_statements</span></span>](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | <span data-ttu-id="7ec31-164">提供一種方法，來追蹤伺服器所執行之所有 SQL 陳述式的執行統計資料。</span><span class="sxs-lookup"><span data-stu-id="7ec31-164">Provides a means for tracking execution statistics of all SQL statements executed by a server.</span></span> |
| [<span data-ttu-id="7ec31-165">postgres\_fdw</span><span class="sxs-lookup"><span data-stu-id="7ec31-165">postgres\_fdw</span></span>](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | <span data-ttu-id="7ec31-166">可用來存取儲存於外部 PostgreSQL 伺服器之資料的外部資料包裝函式</span><span class="sxs-lookup"><span data-stu-id="7ec31-166">Foreign-data wrapper used to access data stored in external PostgreSQL servers</span></span> |

### <a name="postgis"></a><span data-ttu-id="7ec31-167">PostGIS</span><span class="sxs-lookup"><span data-stu-id="7ec31-167">PostGIS</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="7ec31-168">**擴充功能**</span><span class="sxs-lookup"><span data-stu-id="7ec31-168">**Extension**</span></span> | <span data-ttu-id="7ec31-169">**說明**</span><span class="sxs-lookup"><span data-stu-id="7ec31-169">**Description**</span></span> |
|---|---|
| <span data-ttu-id="7ec31-170">[PostGIS](http://www.postgis.net/)、postgis\_topology、postgis\_tiger\_geocoder、postgis\_sfcgal</span><span class="sxs-lookup"><span data-stu-id="7ec31-170">[PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal</span></span> | <span data-ttu-id="7ec31-171">適用於 PostgreSQL 的空間與地理物件。</span><span class="sxs-lookup"><span data-stu-id="7ec31-171">Spatial and geographic objects for PostgreSQL.</span></span> |
| <span data-ttu-id="7ec31-172">address\_standardizer、address\_standardizer\_data\_us</span><span class="sxs-lookup"><span data-stu-id="7ec31-172">address\_standardizer, address\_standardizer\_data\_us</span></span> | <span data-ttu-id="7ec31-173">用來將位址剖析為組成項目。</span><span class="sxs-lookup"><span data-stu-id="7ec31-173">Used to parse an address into constituent elements.</span></span> <span data-ttu-id="7ec31-174">用來支援對位址進行地理編碼的正規化步驟。</span><span class="sxs-lookup"><span data-stu-id="7ec31-174">Used to support geocoding address normalization step.</span></span> |
| [<span data-ttu-id="7ec31-175">pgrouting</span><span class="sxs-lookup"><span data-stu-id="7ec31-175">pgrouting</span></span>](http://pgrouting.org/) | <span data-ttu-id="7ec31-176">擴充 PostGIS / PostgreSQL 地理空間資料庫，以提供地理空間路由功能。</span><span class="sxs-lookup"><span data-stu-id="7ec31-176">Extends the PostGIS / PostgreSQL geospatial database to provide geospatial routing functionality.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7ec31-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ec31-177">Next steps</span></span>
<span data-ttu-id="7ec31-178">沒有看到想要使用擴充功能？</span><span class="sxs-lookup"><span data-stu-id="7ec31-178">Don't see an extension you'd like to use?</span></span> <span data-ttu-id="7ec31-179">請告訴我們。</span><span class="sxs-lookup"><span data-stu-id="7ec31-179">Please let us know.</span></span> <span data-ttu-id="7ec31-180">在我們的[客戶意見反應論壇 (英文)](https://feedback.azure.com/forums/597976-azure-database-for-postgresql) 中投票給現有的要求，或建立新的意見反應和期望。</span><span class="sxs-lookup"><span data-stu-id="7ec31-180">Vote for existing requests or create new feedback and wishes in our [Customer feedback forum](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).</span></span>
