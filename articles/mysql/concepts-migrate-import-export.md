---
title: "aaaImport 和 Azure 資料庫中匯出的 MySQL |Microsoft 文件"
description: "本文件說明常見 Azure Database 中的方式 tooimport 和匯出資料庫的 MySQL 使用 MySQL Workbench 之類的工具。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>使用匯入和匯出移轉您的 MySQL 資料庫
本文件說明使用 MySQL Workbench 兩個常見的方法 tooimporting 和匯出資料 tooan Azure 資料庫的 MySQL 伺服器。 

## <a name="before-you-begin"></a>開始之前
透過這個方式 tooguide toostep，您需要：
- 適用於 MySQL 伺服器的 Azure 資料庫，[使用 Azure 入口網站建立適用於 MySQL 伺服器的 Azure 資料庫](quickstart-create-mysql-server-database-using-azure-portal.md)。
- MySQL Workbench[下載](https://dev.mysql.com/downloads/workbench/)，或另一個 MySQL 工具 tooimport 和匯出。

## <a name="use-common-tools"></a>使用一般工具
使用常見的工具，例如 MySQL Workbench、 Toad 或 Navicat tooremotely 連接和匯入或用於 MySQL 的資料匯出到 Azure 的資料庫。 

MySQL 用戶端電腦與網際網路連線 tooconnect tooAzure 資料庫上使用這類工具。 使用 SSL 加密連線以獲得最佳安全性做法，如[在適用於 MySQL 的 Azure 資料庫中設定 SSL 連線能力](concepts-ssl-connection-security.md)中所述。

請勿需要 toomove 匯入和匯出檔案 tooany 特殊雲端位置，用於 MySQL 移轉 tooAzure 資料庫時。 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>Hello Azure 資料庫的 MySQL 伺服器上建立資料庫
在您要 toomigrate hello 資料所在的 MySQL 伺服器 hello Azure 資料庫上建立空白資料庫。 使用 MySQL Workbench、 Toad 或 Navicat toocreate hello 資料庫之類的工具。 hello 資料庫可以有相同的名稱，如 hello 資料庫包含 hello 傾印的資料，或您可以使用不同的名稱建立資料庫的 hello。

tooget 連線，找出 hello 連接資訊在 hello**屬性**MySQL 的 Azure 資料庫中的窗格。

![在 hello Azure 入口網站中找到 hello 連線資訊](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

新增 hello 連線資訊 tooMySQL Workbench。

![MySQL Workbench 連接字串](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>決定 toouse 匯入及匯出而非傾印和還原技術的時機
使用 MySQL 工具 tooimport 和 hello 下列案例中，將資料庫匯出至 Azure 的 MySQL 資料庫。 在其他情況下，您可能會受益於使用 hello[傾印並還原](concepts-migrate-dump-restore.md)改為方法。 

- 當您需要 tooselectively 選擇從現有的 MySQL 資料庫的一些資料表 tooimport 到 Azure 的 MySQL 資料庫，它的最佳 toouse hello 匯入和匯出的技術。  如此一來，您可以省略任何不必要的資料表從 hello 移轉 toosave 時間和資源。 例如，使用 hello`--include-tables`或`--exclude-tables`參數搭配[mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables)和 hello`--tables`參數搭配[mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables)。
- 移動 hello 資料表以外的資料庫物件時，明確建立的。 包含條件約束 （主索引鍵、 外部索引鍵、 索引）、 檢視、 函數、 程序、 觸發程序，並想 toomigrate 的任何其他資料庫物件。
- 當您從 MySQL 資料庫以外的外部資料來源移轉資料時，建立一般檔案，並且使用 [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html) 來匯入它們。

請確定當您要將資料載入 Azure 資料庫的 MySQL hello 資料庫中的所有資料表，都使用 hello InnoDB 儲存引擎。 Azure 的 MySQL 資料庫支援只 hello InnoDB 儲存引擎，因此它不支援其他儲存引擎。 如果您的資料表需要替代儲存體引擎，可確定 tooconvert 它們 toouse hello InnoDB 引擎格式，才能進行 hello 移轉 tooAzure MySQL 資料庫。 

例如，如果您有使用 hello MyISAM 引擎的 WordPress 或 web 應用程式時，第一次轉換 hello 資料表移轉 hello 資料所 InnoDB 資料表。 然後還原 tooAzure 資料庫的 MySQL。 使用 hello 子句`ENGINE=INNODB`tooset hello 引擎建立的資料表，然後再將 hello 資料傳輸到 hello hello 移轉前的相容資料表。 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>匯入和匯出的效能建議
-   載入資料之前先建立叢集索引和主索引鍵。 以主索引鍵的順序載入資料。 
-   延遲建立次要索引，直到載入資料。 載入之後建立所有次要索引。 
-   載入之前停用外部索引鍵限制式。 停用外部索引鍵檢查會提供顯著的效能提升。 啟用 hello 條件約束，並確認 hello 資料之後 hello 負載 tooensure 參考完整性。
-   平行載入資料。 避免太多平行處理原則會導致您 toohit 資源限制，並監視資源使用可用 hello Azure 入口網站中的 hello 度量。 
-   適當時使用資料分割資料表。

## <a name="import-and-export-by-using-mysql-workbench"></a>使用 MySQL Workbench 匯入和匯出
有兩種方式 tooexport 和匯入資料 MySQL 工作臺 中。 每一種適用於不同用途。 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>資料表資料匯出和匯入精靈，從 hello 物件瀏覽器的快顯功能表
![Hello 物件瀏覽器的快顯功能表上的 MySQL Workbench 精靈](./media/concepts-migrate-import-export/p1.png)

資料表資料的 hello 精靈支援匯入和匯出作業所使用的 CSV 和 JSON 檔案。 它們包含數個設定選項，例如分隔符號、資料行選取和編碼選取項目。 您可以對本機或遠端連線的 MySQL 伺服器執行每個精靈。 hello 匯入動作包括資料表、 資料行和型別對應。 

您可以從 hello 物件瀏覽器的快顯功能表存取這些精靈，以滑鼠右鍵按一下資料表。 然後選擇 [資料表資料匯出精靈] 或 [資料表資料匯入精靈]。 

#### <a name="table-data-export-wizard"></a>資料表資料匯出精靈
hello 下列範例會匯出 hello 資料表 tooa CSV 檔案： 
1. 以滑鼠右鍵按一下 匯出的 hello 資料庫 toobe hello 資料表。 
2. 選取 [資料表資料匯出精靈]。 選取 hello 資料行 toobe 匯出時，資料列位移 （如果有的話），並計算 （如果有的話）。 
3. 在 hello**選取匯出的資料**頁面上，按一下**下一步**。 選取 hello 檔案路徑、 CSV 或 JSON 檔案類型。 也可以選取 hello 行分隔符號的字串，與欄位分隔符號封入方法。 
4. 在 hello**選取輸出檔案位置**頁面上，按一下**下一步**。 
5. 在 hello**匯出資料**頁面上，按一下**下一步**。

#### <a name="table-data-import-wizard"></a>資料表資料匯入精靈
hello 下列範例會匯入 hello 資料表從 CSV 檔案：
1. 以滑鼠右鍵按一下 匯入的 hello 資料庫 toobe hello 資料表。 
2. 瀏覽 tooand 選取 hello 匯入，CSV 檔案 toobe，然後按一下**下一步**。 
3. 選取 hello 目的地資料表 （新的或現有），並選取或清除 hello**匯入前的截斷資料表**核取方塊。 按一下 [下一步] 。
4. 選取編碼方式和 hello 的資料行 toobe 匯入，然後再按一下**下一步**。 
5. 在 hello**匯入資料**頁面上，按一下**下一步**。 hello 精靈會據以匯入 hello 資料。

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>SQL 資料匯出和匯入精靈，從 hello 導覽器窗格
使用精靈 tooexport 或匯入 SQL 從 MySQL Workbench 產生或從 hello mysqldump 命令產生。 從 hello 存取這些精靈**導覽**窗格，或選取**伺服器**從 hello 主功能表。 然後選取 [資料匯出] 或 [資料匯入]。 

#### <a name="data-export"></a>資料匯出
![使用 hello 導覽器窗格的 MySQL Workbench 資料匯出](./media/concepts-migrate-import-export/p2.png)

您可以使用 hello**資料匯出**索引標籤上的 tooexport MySQL 資料。 
1. 選取您想 tooexport、 選擇性地從每個結構描述中，選取物件資料表的特定結構描述，產生 hello 匯出每個結構描述。 設定選項包括匯出 tooa 專案資料夾或獨立的 SQL 檔案、 傾印預存的常式和事件，或略過資料表資料。 
 
   或者，使用**匯出結果集**tooexport 特定結果集以 hello SQL 編輯器 tooanother 的格式，例如 CSV、 JSON、 HTML 和 XML。 
3. 選取 hello 資料庫物件 tooexport，並設定 hello 相關選項。
4. 按一下**重新整理**tooload hello 目前的物件。
5. 或者，開啟 hello**進階選項**toorefine hello 匯出作業索引標籤上。 例如，新增資料表鎖定、使用 replace 而不是 insert 陳述式，以及使用反引號字元將識別項括起來。
6. 按一下**開始匯出**toobegin hello 匯出程序。


#### <a name="data-import"></a>資料匯入
![使用管理導覽器的 MySQL Workbench 資料匯入](./media/concepts-migrate-import-export/p3.png)

您可以使用 hello**資料匯入**tooimport 索引標籤上，或從 hello 資料匯出作業或 hello mysqldump 命令還原匯出的資料。 
1. 選擇 hello 專案資料夾或獨立的 SQL 檔案中，選擇 hello 結構描述 tooimport，或選擇**新增**toodefine 新的結構描述。 
2. 按一下**開始匯入**toobegin hello 匯入程序。

## <a name="next-steps"></a>後續步驟
至於另一個移轉方法，請參閱[在適用於 MySQL 的 Azure 資料庫中使用傾印和還原來移轉 MySQL 資料庫](concepts-migrate-dump-restore.md)。 
