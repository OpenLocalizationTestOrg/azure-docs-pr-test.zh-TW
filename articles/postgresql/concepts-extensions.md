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
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>適用於 PostgreSQL 的 Azure 資料庫中的 PostgreSQL 擴充功能
PostgreSQL 提供 hello 資料庫使用擴充功能的能力 tooextend hello 功能。 擴充功能允許多個相關的 SQL 物件 toobe 單一封裝中配套在一起，可載入或從您的資料庫，使用單一命令中移除。 一次載入 hello 資料庫的擴充功能可以運作一樣內建的功能。 如需 PostgreSQL 擴充功能的詳細資訊，請參閱[將相關物件封裝成擴充功能 (英文)](https://www.postgresql.org/docs/9.6/static/extend-extensions.html)。

## <a name="how-toouse-postgresql-extensions"></a>如何 toouse PostgreSQL 延伸模組嗎？
PostgreSQL 延伸模組需要 toobe 安裝您的資料庫，才能使用它們。 執行 tooinstall 特定的副檔名為[建立副檔名](https://www.postgresql.org/docs/9.6/static/sql-createextension.html)命令從 psql 工具 tooload hello 封裝的物件至您的資料庫。

適用於 PostgreSQL 的 Azure 資料庫支援的部分重要擴充功能如此處所列。 超出 hello 列示，不支援其他擴充功能。 您無法針對適用於 PostgreSQL 的 Azure 資料庫服務，自行建立擴充功能。

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>適用於 PostgreSQL 的 Azure 資料庫支援的擴充功能
hello 以下表格列出 hello 標準 PostgreSQL 擴充功能會針對 PostgreSQL 目前支援的 Azure 資料庫。 您也可以藉由查詢 pg\_available\_extensions 來取得此資訊。 

### <a name="data-types-extensions"></a>資料類型擴充功能

> [!div class="mx-tableFixed"]
| **擴充功能** | **說明** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | 提供不區分大小寫的字元字串類型 |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | 提供用來儲存索引鍵/值組之集合的資料類型 |

### <a name="functions-extensions"></a>函數擴充功能

> [!div class="mx-tableFixed"]
| **擴充功能** | **說明** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | 提供數個函式 toodetermine 相似與字串之間的距離。 |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | 提供函數和運算子來操作無 null 的整數陣列。 |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | 提供密碼編譯函數 |
| [pg\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | 依時間或識別碼來管理資料分割資料表 |
| [pg\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | 提供判斷 hello 根據三字母組比對英數字元的文字相似度的函數和運算子 |
| [uuid-ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | 產生通用唯一識別碼 (UUID) |

### <a name="full-text-search-extensions"></a>全文檢索搜尋擴充功能

> [!div class="mx-tableFixed"]
| **擴充功能** | **說明** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | 文字搜尋字典，可從詞彙中移除重音符號 (變音符號)。 |

### <a name="index-types-extensions"></a>索引類型擴充功能

> [!div class="mx-tableFixed"]
| **擴充功能** | **說明** |
|---|---|
| [btree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | 提供範例 GIN 運算子類別，可針對特定資料類型實作類似 B 型樹狀結構的行為。 |
| [btree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | 提供可實作 B 型樹狀結構的 GiST 索引運算子類別。 |

### <a name="language-extensions"></a>語言擴充功能

> [!div class="mx-tableFixed"]
| **擴充功能** | **說明** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | PL/pgSQL 可載入的程序性語言 |

### <a name="miscellaneous-extensions"></a>其他擴充功能

> [!div class="mx-tableFixed"]
| **擴充功能** | **說明** |
|---|---|
| [pg\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | 提供方法來檢查即時 hello 共用緩衝區快取中的情況。 |
| [pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | 會提供資料的方式 tooload 關聯至 hello 緩衝快取。 |
| [pg\_stat\_statements](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | 提供一種方法，來追蹤伺服器所執行之所有 SQL 陳述式的執行統計資料。 |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | 使用 tooaccess 資料儲存在外部 PostgreSQL 伺服器中的外部資料包裝函式 |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **擴充功能** | **說明** |
|---|---|
| [PostGIS](http://www.postgis.net/)、postgis\_topology、postgis\_tiger\_geocoder、postgis\_sfcgal | 適用於 PostgreSQL 的空間與地理物件。 |
| address\_standardizer、address\_standardizer\_data\_us | 使用的 tooparse 組成項目位址。 使用 toosupport 地理編碼位址正規化步驟。 |
| [pgrouting](http://pgrouting.org/) | 擴充 hello PostGIS / PostgreSQL geospatial 資料庫 tooprovide geospatial 路由功能。 |

## <a name="next-steps"></a>後續步驟
沒看見您想要 toouse 擴充功能嗎？ 請告訴我們。 在我們的[客戶意見反應論壇 (英文)](https://feedback.azure.com/forums/597976-azure-database-for-postgresql) 中投票給現有的要求，或建立新的意見反應和期望。
