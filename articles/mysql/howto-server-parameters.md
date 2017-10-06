---
title: "aaaHow tooConfigure 用於 MySQL 的 Azure 資料庫中的伺服器參數 |Microsoft 文件"
description: "本文說明如何在 Azure 資料庫中用於 MySQL 的 tooconfigure 可用的伺服器參數 hello Azure 入口網站。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>如何在 Azure 資料庫中用於 MySQL 的 tooconfigure 伺服器參數 hello Azure 入口網站

MySQL 的 Azure 資料庫支援某些伺服器參數的組態。 本文說明如何 tooconfigure hello Azure 入口網站和清單 hello 使用這些參數支援參數、 hello 預設值和 hello 有效值範圍。 並非所有伺服器參數皆可調整。 支援 hello 這裡所列。

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>瀏覽 tooServer 參數刀鋒視窗，在 Azure 入口網站

登入 toohello Azure 入口網站，然後按一下 您的 Azure 資料庫的 MySQL 伺服器的名稱。 在 hello**設定**區段中，按一下**伺服器參數**tooopen hello 伺服器參數刀鋒視窗中的 hello Azure MySQL 資料庫。

![Azure 入口網站伺服器參數刀鋒視窗](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>可設定的伺服器參數清單

hello 下表列出目前支援的 hello 伺服器參數。 您可以根據 tooyour 應用程式的需求設定 hello 參數。

> [!div class="mx-tableFixed"]
|參數名稱|預設值|範圍|描述|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|控制項多少百萬分之一秒為單位 hello 二進位記錄檔認可等候同步處理 hello 二進位記錄檔檔案 toodisk 之前。|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|hello 的中止 hello binlog-群組-認可-sync-延遲所指定的目前延遲之前的交易 toowait 的數目上限。|
|character_set_server|LATIN1|BIG5、UTF8MB4 等。|使用 charset_name 做為 hello 預設伺服器的字元集。|
|div_precision_increment|4|0-30|依 hello 的除法運算的結果的哪些 tooincrease hello 小數位數的數字的數目。|
|group_concat_max_len|1024|4-16777216|以位元組為單位的 hello GROUP_CONCAT() 結果的長度允許上限。|
|innodb_adaptive_hash_index|開啟|開啟、關閉|啟用還是停用 innodb 彈性雜湊索引。|
|innodb_lock_wait_timeout|50|1-3600|hello 以秒為單位的時間長度 InnoDB 交易等候的資料列鎖定後才放棄。|
|interactive_timeout|1800|10-1800|活動的互動式連接關閉之前等候的秒 hello 伺服器數目。|
|log_bin_trust_function_creators|關|開啟、關閉|此變數適用於啟用二進位記錄時。 它會控制建立者可以是預存函式是否信任不會造成不安全的事件 toobe toohello 二進位記錄檔中寫入 toocreate 儲存函式。|
|log_queries_not_using_indexes|關|開啟、關閉|記錄檔查詢的預期 tooretrieve 所有資料列 tooslow 查詢記錄檔。|
|log_slow_admin_statements|關|開啟、關閉|包含緩慢系統管理中陳述式撰寫 toohello 慢速查詢記錄檔的 hello 陳述式。|
|log_throttle_queries_not_using_indexes|0|0-4294967295|限制 hello 每分鐘且可以寫入 toohello 慢速查詢記錄檔的這類查詢的數目。|
|long_query_time|10|1-1E+100|如果查詢時間長於此秒數，hello 伺服器就會遞增 hello Slow_queries 狀態變數。|
|max_allowed_packet|536870912|1024-1073741824|hello 一個封包或任何中繼產生字串或傳送嗨 mysql_stmt_send_long_data() C 應用程式開發介面函式的任何參數的大小上限。|
|min_examined_row_limit|0|0-18446744073709551615|記錄具有大於設定的 hello hello 慢速查詢記錄檔資料列數目的查詢。 |
|server_id|3293747068|1000-4294967295|複寫 toogive 中所用的 hello 伺服器識別碼每一個主要和從屬的唯一識別。|
|slave_net_timeout|60|30-3600|hello 數目更多的資料，從 hello 主要 hello 從屬會考慮 hello 連接中斷之前, 的秒數 toowait hello 讀取，會中止，而且會嘗試 tooreconnect。|
|slow_query_log|關|開啟、關閉|啟用或停用 hello 慢速查詢記錄檔。|
|sql_mode|已選取 0|ALLOW_INVALID_DATES、IGNORE_SPACE 等。|目前伺服器 SQL 模式 hello。|
|time_zone|系統|範例：-8:00、+05:30|hello 伺服器的時區。|
|wait_timeout|120|60-240|活動的非互動式連線關閉之前等待的秒 hello 伺服器的 hello 次數。|

## <a name="next-steps"></a>後續步驟
- [適用於 MySQL 的 Azure 資料庫的連線庫](concepts-connection-libraries.md)
