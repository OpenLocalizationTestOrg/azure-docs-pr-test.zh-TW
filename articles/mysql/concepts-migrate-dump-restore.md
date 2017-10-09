---
title: "您 MySQL 資料庫使用傾印並還原 Azure 資料庫中的 MySQL aaaMigrate |Microsoft 文件"
description: "這篇文章會說明兩個常見的方式 tooback 向上和 Azure 資料庫中的還原資料庫的 MySQL、 使用 mysqldump、 MySQL Workbench 和 PHPMyAdmin 之類的工具。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: d05d483ff53483df8e005eae2d9a4f8190e8f663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-tooazure-database-for-mysql-using-dump-and-restore"></a>用於使用傾印和還原 MySQL 移轉您的 MySQL 資料庫 tooAzure 資料庫
本文說明兩個常見的方式 tooback 向上並還原 Azure 資料庫中的資料庫的 MySQL
- 傾印與還原自 hello 命令列 （使用 mysqldump） 
- 使用 PHPMyAdmin 傾印和還原 

## <a name="before-you-begin"></a>開始之前
透過這個方式 tooguide toostep，您需要 toohave:
- [建立適用於 MySQL 的 Azure 資料庫伺服器 - Azure 入口網站](quickstart-create-mysql-server-database-using-azure-portal.md)
- 已安裝於電腦上的 [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html) 命令列公用程式。
- MySQL Workbench [MySQL Workbench 下載](https://dev.mysql.com/downloads/workbench/)，Toad、 Navicat 或其他第三方 MySQL 的工具有 toodo 傾印和還原命令。

## <a name="use-common-tools"></a>使用一般工具
使用常用的公用程式和工具，例如 MySQL Workbench、 mysqldump、 Toad 或 Navicat tooremotely 連接，並將資料還原到 Azure 資料庫，用於 MySQL。 MySQL 用戶端電腦與網際網路連線 tooconnect toohello Azure 資料庫上使用這類工具。 如需使用 SSL 加密連接的最佳安全性作法，請參閱[在適用於 MySQL 的 Azure 資料庫中設定 SSL 連線能力](concepts-ssl-connection-security.md)。 For MySQL 移轉 tooAzure 資料庫時不需要 toomove hello 傾印檔案 tooany 特殊雲端位置。 

## <a name="common-uses-for-dump-and-restore"></a>傾印和還原的常見用途
您可以使用例如 mysqldump 和 mysqlpump toodump 和負載的資料庫到 Azure 的 MySQL 資料庫的 MySQL 公用程式在幾個常見的案例。 在其他情況下，您可以使用 hello[匯入和匯出](concepts-migrate-import-export.md)改為方法。

- 當您要移轉 hello 整個資料庫時，使用資料庫傾印。 移動大量的 MySQL 資料，或者您想 toominimize 服務中斷即時網站或應用程式時，就會保留這項建議。 
-  請確定 hello 資料庫中的所有資料表資料載入用於 MySQL 的 Azure 資料庫時，請都使用 hello InnoDB 儲存引擎。 適用於 MySQL 的 Azure 資料庫僅支援 InnoDB 儲存引擎，因此不支援其他儲存引擎。 如果使用其他儲存體引擎設定您的資料表，將它們轉換成 hello InnoDB 引擎格式，才能移轉 tooAzure 資料庫的 MySQL。
   例如，如果您的 WordPress 或 WebApp 使用 hello MyISAM 資料表，第一次轉換這些資料表移轉至 InnoDB 格式，再還原 tooAzure 資料庫的 MySQL。 使用 hello 子句`ENGINE=InnoDB`tooset hello 引擎使用時建立新的資料表，然後 hello 資料傳送到 hello hello 還原之前的相容資料表。 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```
- tooavoid 任何相容性問題，請確定的 hello hello 來源和目的地系統使用相同版本的 MySQL 資料庫傾印時。 比方說，如果現有的 MySQL server 5.7 版，您應該移轉設定的 MySQL toorun 版本 5.7 tooAzure 資料庫。 hello`mysql_upgrade`命令會在 Azure 資料庫的 MySQL 伺服器無法運作，並不支援。 如果您需要 tooupgrade MySQL 版本之間，第一次傾印，或是將較低版本的資料庫匯出到您自己的環境中較高版本的 MySQL。 然後執行 `mysql_upgrade`，之後再嘗試移轉至適用於 MySQL 的 Azure 資料庫。

## <a name="performance-considerations"></a>效能考量
take 請注意，一個傾印大型資料庫時，這些考量 toooptimize 效能：
-   使用 hello `exclude-triggers` mysqldump 時傾印資料庫中的選項。 排除傾印檔案 tooavoid hello 觸發程序命令 hello 資料還原期間引發的觸發程序。 
-   避免 hello `single-transaction` mysqldump 時傾印非常龐大的資料庫中的選項。 傾印在單一交易中的許多資料表會導致額外的儲存體和記憶體資源 toobe 還原期間耗用，而且可能會導致效能延遲或資源條件約束。
-   使用多重值插入時傾印資料庫時，載入 SQL toominimize 陳述式執行額外負荷。 使用 mysqldump 公用程式所產生的傾印檔案時，預設會啟用多重值插入。 
-  使用 hello `order-by-primary` mysqldump 時傾印的資料庫，以便 hello 資料編寫指令碼中主索引鍵的順序中的選項。
-   使用 hello`disable-keys`中 mysqldump 傾印 toodisable foreign key 條件約束之前載入的資料時的選項。 停用外部索引鍵檢查會提供效能提升。 啟用 hello 條件約束，並確認 hello 資料之後 hello 負載 tooensure 參考完整性。
-   適當時使用資料分割資料表。
-   平行載入資料。 避免太多平行處理原則會導致您 toohit 資源限制，並監視資源使用 hello hello Azure 入口網站中可用的度量。 
-   使用 hello`defer-table-indexes`中 mysqlpump 傾印資料庫，這樣可以建立索引執行之後載入資料表資料時的選項。

## <a name="create-a-backup-file-from-hello-command-line-using-mysqldump"></a>建立備份檔案從 hello 命令列使用 mysqldump
設定現有的 MySQL 資料庫 hello 本機內部部署伺服器上或在虛擬機器中，執行下列命令的 hello tooback: 
```bash
$ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
```

hello 參數 tooprovide 如下：
- [uname] 您的資料庫使用者名稱 
- 您的資料庫的 [傳遞] hello 密碼 （請注意-p 與 hello 密碼之間沒有空格） 
- 資料庫 [dbname] hello 名稱 
- 資料庫備份 [backupfile.sql] hello 檔名 
- [-opt] hello mysqldump 選項 

比方說，tooback 資料庫名為 'testdb' 的 MySQL 伺服器 hello 使用者名稱為 'testuser' 與沒有密碼 tooa 檔案 testdb_backup.sql，請使用下列命令的 hello。 hello 命令會備份 hello`testdb`資料庫檔案，稱為`testdb_backup.sql`，其中包含所有 hello SQL 陳述式需要 toore-建立 hello 資料庫。 

```bash
$ mysqldump -u root -p testdb > testdb_backup.sql
```
在您的資料庫 tooback 向上 tooselect 特定資料表，以空格分隔清單 hello 資料表名稱。 例如，從 hello 'testdb' 的唯一 table1 和 table2 資料表 tooback 依照此範例： 
```bash
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

多個資料庫使用 hello-次 tooback 資料庫切換，並以空格分隔的清單 hello 資料庫名稱。 
```bash
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```
tooback hello 伺服器一次中的所有 hello 資料庫，您應該使用 hello-所有資料庫選項。
```
$ mysqldump -u root -p --all-databases > alldb_backup.sql 
```

## <a name="create-a-database-on-hello-target-azure-database-for-mysql-server"></a>MySQL 伺服器 hello 目標 Azure 資料庫上建立資料庫
您要 toomigrate hello 資料所在的 MySQL 伺服器 hello 目標 Azure 資料庫上建立空白資料庫。 使用 MySQL Workbench、 Toad 或 Navicat toocreate hello 資料庫之類的工具。 hello 資料庫可以有 hello 自主的 hello 傾印資料的資料庫名稱相同的 hello 或您可以使用不同的名稱建立資料庫。

tooget 連線，您的 Azure 資料庫中找到 MySQL hello hello 內容 頁面上的連接資訊。
![在 hello Azure 入口網站中找到 hello 連線資訊](./media/concepts-migrate-dump-restore/1_server-properties-name-login.png)

Hello 連接將資訊加入至您的 MySQL Workbench。
![MySQL Workbench 連接字串](./media/concepts-migrate-dump-restore/2_setup-new-connection.png)


## <a name="restore-your-mysql-database-using-command-line-or-mysql-workbench"></a>使用命令列或 MySQL Workbench 來還原 MySQL 資料庫
一旦您已經建立 hello 目標資料庫，您可以使用 hello mysql 命令或 MySQL Workbench toorestore hello 資料至特定的 hello 新建資料庫從 hello 傾印檔案。
```bash
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```
在此範例中，再將 hello 資料還原至新的 MySQL 伺服器 hello 目標 Azure 資料庫上建立資料庫的 hello。
```bash
$ mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p testdb < testdb_backup.sql
```

## <a name="export-using-phpmyadmin"></a>使用 PHPMyAdmin 匯出
tooexport，您可以使用 hello 通用工具 phpMyAdmin，您可能已經有安裝在本機環境中。 tooexport 使用 PHPMyAdmin MySQL 資料庫：
- 開啟 phpMyAdmin。
- 選取您的資料庫。 按一下 hello hello hello 左邊的清單中的資料庫名稱。 
- 按一下 hello**匯出**連結。 新的頁面會顯示資料庫 tooview hello 傾印。
- 在 hello 匯出區域中，按一下 hello**全選**連結 toochoose hello 資料表在資料庫中的。 
- 在 hello SQL 選項 區域中，按一下 hello 適當的選項。 
- 按一下 hello**將儲存為檔案**選項和 hello 對應壓縮選項，然後再按一下 [hello**移**] 按鈕。 提示您 toosave hello 檔案儲存在本機應該會出現一個對話方塊。

## <a name="import-using-phpmyadmin"></a>使用 PHPMyAdmin 匯入
匯入您的資料庫是類似 tooexporting。 Hello 下下列動作：
- 開啟 phpMyAdmin。 
- 在 hello phpMyAdmin 安裝程式 頁面上，按一下 **新增**tooadd 您的 Azure 資料庫的 MySQL 伺服器。 提供 hello 連接詳細資料和登入資訊。
- 建立適當命名的資料庫，並選取 hello 左邊囉 」 畫面上。 toorewrite hello 現有的資料庫，按一下 hello 資料庫名稱、 選取所有 hello 核取方塊旁 hello 資料表名稱，然後都選取**卸除**toodelete hello 現有的資料表。 
- 按一下 hello **SQL**連結 tooshow hello 頁面可以在此輸入 SQL 命令中或上傳您的 SQL 檔案。 
- 使用 hello**瀏覽**按鈕 toofind hello 資料庫檔案。 
- 按一下 hello**移**按鈕 tooexport hello 備份，執行 hello SQL 命令，然後重新建立您的資料庫。

## <a name="next-steps"></a>後續步驟
[連接應用程式 tooAzure 資料庫的 MySQL](./howto-connection-string.md)
