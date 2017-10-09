---
title: "aaaServer Azure 資料庫中記錄檔取得 PostgreSQL |Microsoft 文件"
description: "在適用於 PostgreSQL 的 Azure 資料庫中產生查詢和錯誤記錄。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>適用於 PostgreSQL 的 Azure 資料庫中的伺服器記錄 
適用於 PostgreSQL 的 Azure 資料庫會產生查詢和錯誤記錄。 不過，不支援存取 tootransaction 記錄檔。 這些記錄檔可以是使用的 tooidentify、 疑難排解與修復組態錯誤和效能次佳。 如需詳細資訊，請參閱[錯誤報告和記錄 (英文)](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html)。

## <a name="access-server-logs"></a>存取伺服器記錄
您可以列出並下載 Azure PostgreSQL server 錯誤記錄檔使用 hello Azure 入口網站， [Azure CLI](howto-configure-server-logs-using-cli.md)和 Azure REST Api。

## <a name="log-retention"></a>記錄保留
您可以設定使用的系統記錄檔的 hello 保留週期**記錄\_保留\_期間**與您的伺服器相關聯的參數。 這個參數的 hello 單位為的天 （需要 tooconfirm）。 hello 預設值為 3 天。 hello 最大值為 7 天。 請注意您的伺服器必須具有足夠配置的儲存體 toocontain hello 保留記錄檔。
hello 記錄檔會旋轉每 1 小時] 或 [100 MB 的大小、 何者較早。

## <a name="configure-logging-for-azure-postgresql-server"></a>設定 Azure PostgreSQL 伺服器的記錄
您可以針對伺服器啟用查詢記錄和錯誤記錄。 錯誤記錄可包含自動清空、連接和檢查點資訊。

您可以藉由設定兩個伺服器參數來啟用 PostgreSQL DB 執行個體的查詢記錄︰log\_statement 和 log\_min\_duration\_statement。

hello**記錄\_陳述式**參數用於控制記錄哪一個 SQL 陳述式。 我們建議您將這個參數設定為太***所有***toolog 所有陳述式; hello 預設值是 none （需要 tooconfirm）。

hello**記錄\_min\_持續時間\_陳述式**參數設定以毫秒為單位的記錄陳述式 toobe hello 限制。 記錄執行時間超過 hello 參數設定的所有 SQL 陳述式。 這個參數 (需要 tooconfirm) 預設為停用和設定 toominus 1 (-1)。 啟用此參數，有助於追蹤應用程式中未最佳化的查詢。

hello**記錄\_min\_訊息**可讓您 toocontrol toohello server 記錄檔寫入的訊息層級。 hello 預設為警告。 （需要 tooconfirm）

如需有關這些設定的詳細資訊，請參閱[錯誤報告和記錄 (英文)](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) 文件。 若要特別設定適用於 PostgreSQL 的 Azure 資料庫伺服器參數，請參閱[適用於 PostgreSQL 的 Azure 資料庫中的伺服器記錄](concepts-server-logs.md)。

## <a name="next-steps"></a>後續步驟
- tooaccess 記錄使用 Azure CLI 命令列介面，請參閱 <<c0> [ 使用 Azure CLI 設定及存取伺服器記錄檔](howto-configure-server-logs-using-cli.md)
- 如需伺服器參數的詳細資訊，請參閱[使用 Azure CLI 自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)。