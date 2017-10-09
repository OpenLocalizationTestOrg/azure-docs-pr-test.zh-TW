---
title: "適用於 PostgreSQL 的 Azure 資料庫的連線庫 | Microsoft Docs"
description: "本文說明幾個程式庫和編碼 PostgreSQL tooconnect 應用程式和查詢 Azure 資料庫時，開發人員可以使用的驅動程式。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/15/2017
ms.openlocfilehash: 1f7234499d8abe37f8de9008e3158765b1fb0bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connection-libraries-for-azure-database-for-postgresql"></a>適用於 PostgreSQL 的 Azure 資料庫的連線庫
本主題列出程式庫和驅動程式的開發人員用於 PostgreSQL 的程式設計應用程式 tooconnect 和查詢 Azure 資料庫。

## <a name="client-interfaces"></a>用戶端介面
大部分語言的用戶端程式庫 tooconnect tooPostgreSQL 伺服器外部專案，而且獨立散發。 Windows、Linux 和 Mac 平台均支援這些程式庫。 列出的 hello 熱門的用戶端驅動程式：

| **語言** | **用戶端介面** | **其他資訊** | **下載** |
|--------------|----------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------------|
| Python | [psycopg](http://initd.org/psycopg/) | DB API 2.0 相容 | [下載](http://initd.org/psycopg/download/) |
| PHP | [php-pgsql](https://php.net/manual/en/book.pgsql.php) | 資料庫擴充功能 | [安裝](https://secure.php.net/manual/en/pgsql.installation.php) |
| Node.js | [Pg npm 封裝](https://www.npmjs.com/package/pg) | 單純的 JavaScript 非封鎖用戶端 | [安裝](https://www.npmjs.com/package/pg) |
| Java | [JDBC](http://jdbc.postgresql.org/) | Type 4 JDBC 驅動程式 | [下載](https://jdbc.postgresql.org/download.html)  |
| Ruby | [Pg gem](https://deveiate.org/code/pg/) | Ruby 介面 | [下載](https://rubygems.org/downloads/pg-0.20.0.gem) |
| Go | [Package pq](https://godoc.org/github.com/lib/pq) | 單純的 Go postgres 驅動程式 | [安裝](https://github.com/lib/pq/blob/master/README.md) |
| C\#/ .NET | [Npgsql](http://www.npgsql.org/) | ADO.NET 資料提供者 | [下載](https://www.microsoft.com/net/) |
| ODBC | [psqlODBC](https://odbc.postgresql.org/) | ODBC 驅動程式 | [下載](http://www.postgresql.org/ftp/odbc/versions/) |
| C | [libpq](https://www.postgresql.org/docs/9.6/static/libpq.html) | 主要的 C 語言介面 | 已包括 |
| C++ | [libpqxx](http://pqxx.org/) | 新樣式的 C++ 介面 | [下載](http://pqxx.org/download/software/) |

## <a name="next-steps"></a>後續步驟
閱讀有關這些快速入門 tooconnect 和查詢使用您所選擇的語言 PostgreSQL 資料庫 Azure:

[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET (C#)](./connect-csharp.md)
