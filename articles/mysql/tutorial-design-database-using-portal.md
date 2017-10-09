---
title: "第一個 Azure 資料庫的 MySQL 資料庫-Azure 入口網站的 aaaDesign |Microsoft 文件"
description: "本教學課程說明如何 toocreate 和管理 MySQL 伺服器的 Azure 資料庫，以及使用 Azure 入口網站的資料庫。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>設計您第一個適用於 MySQL 資料庫的 Azure 資料庫
Azure MySQL 資料庫是受管理的服務，可讓您 toorun、 管理及調整 hello 雲端中的高可用性 MySQL 資料庫。 使用 hello Azure 入口網站，可以輕鬆地管理您的伺服器及設計資料庫。

在此教學課程中，您可以使用 hello Azure 入口網站 toolearn 如何以：

> [!div class="checklist"]
> * 建立適用於 MySQL 的 Azure 資料庫
> * Hello 伺服器防火牆設定
> * 使用 mysql 命令列工具 toocreate 資料庫
> * 載入範例資料
> * 查詢資料
> * 更新資料
> * 還原資料

## <a name="sign-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站
開啟我的最愛網頁瀏覽器，並造訪 hello [Microsoft Azure 入口網站](https://portal.azure.com/)。 輸入認證 toosign toohello 入口網站中。 hello 預設檢視是服務儀表板。

## <a name="create-an-azure-database-for-mysql-server"></a>建立適用於 MySQL 的 Azure 資料庫伺服器
建立的「適用於 MySQL 的 Azure 資料庫」伺服器會有一組已定義的[計算和儲存體](./concepts-compute-unit-and-storage.md)資源。 hello 伺服器內建立[Azure 資源群組](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)。

1. 瀏覽過**資料庫** > **Azure 資料庫的 MySQL**。 如果找不到 MySQL Server 底下**資料庫**分類中，按一下 **查看所有**tooshow 所有可用的資料庫服務。 您也可以輸入**Azure 資料庫的 MySQL**在 hello 搜尋方塊 tooquickly 尋找 hello 服務。
![2-1 瀏覽 tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. 按一下 Azure Database for MySQL 圖格，然後按一下建立。

在本例中，填寫 hello Azure 資料庫的 MySQL 表單以 hello 下列資訊：

| **設定** | **建議的值** | **欄位描述** |
|---|---|---|
| *伺服器名稱* | myserver4demo  | 伺服器名稱的全域唯一 toobe。 |
| *訂用帳戶* | mysubscription | 從 hello 下拉式清單中選取訂用帳戶。 |
| *資源群組* | myresourcegroup | 建立資源群組或使用現有的資源群組。 |
| *伺服器管理員登入* | myadmin | 設定管理帳戶名稱。 |
| *密碼* |  | 設定強式管理帳戶密碼。 |
| *確認密碼* |  | 確認 hello 管理帳戶的密碼。 |
| *位置* |  | 選取可用的區域。 |
| *版本* | 5.7 | 選擇 hello 最新版本。 |
| *設定效能* | 基本、50 個計算單位、50 GB  | 選擇 **[定價層]** 、 **[計算單位]** 、**[儲存體]** \(GB) ，然後按一下 **[確定]**。 |
| *Pin tooDashboard* | 勾選 | 建議 toocheck 此方塊，讓您輕鬆地更新版本上可能會發現 hello 伺服器 |
然後按一下 [ **建立**]。 在一兩分鐘，新的 Azure 資料庫的 MySQL 伺服器 hello 雲端中執行。 您可以按一下**通知**hello 工具列 toomonitor hello 部署程序上的按鈕。

## <a name="configure-firewall"></a>設定防火牆
「適用於 MySQL 的 Azure 資料庫」會受到防火牆保護。 根據預設，將會拒絕所有連線 toohello 伺服器和 hello 資料庫 hello 伺服器內。 連接 tooAzure 資料庫的 MySQL hello 第一次之前，先設定 hello 防火牆 tooadd hello 用戶端機器的公用網路的 IP 位址 （或 IP 位址範圍）。

1. 按一下您新建立的伺服器，然後按一下連線安全性。
   ![3-1 連線安全性](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. 您可以在這裡 [新增我的 IP]，或設定防火牆規則。 請記住 tooclick**儲存**建立 hello 規則之後。
您現在可以連接 toohello 伺服器使用 mysql 命令列工具或 MySQL Workbench GUI 工具。

> [!TIP]
> 「適用於 MySQL 的 Azure 資料庫」伺服器會透過連接埠 3306 進行通訊。 如果您嘗試 tooconnect 從公司網路內，透過連接埠 3306 輸出流量可能不允許您的網路防火牆。 如果是這樣，您無法連接 tooAzure MySQL 伺服器，除非您的 IT 部門會開啟連接埠 3306。

## <a name="get-connection-information"></a>取得連線資訊
完整的 get hello**伺服器名稱**和**伺服器系統管理員登入名稱**MySQL 伺服器 hello Azure 入口網站從 Azure 資料庫。 您使用 hello 完整的伺服器名稱 tooconnect tooyour 伺服器使用 mysql 命令列工具。 

1. 在[Azure 入口網站](https://portal.azure.com/)，按一下 [**所有資源**從 hello 左側]、 類型 hello 名稱，並搜尋您的 Azure 資料庫的 MySQL 伺服器。 選取 hello 伺服器名稱 tooview hello 詳細資料。

2. 在 hello 設定下標題之下，按一下**屬性**。 記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。 您可以按一下 hello 複製按鈕下一步 tooeach 欄位 toocopy toohello 剪貼簿。
   ![4-2 伺服器屬性](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

在此範例中，hello 伺服器名稱是*myserver4demo.mysql.database.azure.com*，hello server 系統管理員登入，且 *myadmin@myserver4demo* 。

## <a name="connect-toohello-server-using-mysql"></a>使用 mysql toohello 伺服器連接
使用[mysql 命令列工具](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)tooestablish MySQL 伺服器的連線 tooyour Azure 資料庫。 您可以執行 hello mysql 命令列工具，從 hello 瀏覽器中的 hello Azure 雲端殼層或您自己的電腦在本機使用已安裝的 mysql 工具。 toolaunch hello Azure 雲端 Shell 中，按一下 hello`Try It`工具列上的程式碼區塊，在本文中，或請造訪 hello Azure 入口網站，然後按一下 hello `>_` hello 頂端工具列右側的圖示。 

輸入 hello 命令 tooconnect:
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>建立空白資料庫
一旦您已連線的 toohello 伺服器，建立具有空白資料庫 toowork。
```sql
CREATE DATABASE mysampledb;
```

在 hello 提示字元中執行下列命令 tooswitch 連線 toothis 新建資料庫的 hello:
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Hello 資料庫中建立資料表
您現在知道如何 tooconnect toohello Azure 資料庫的 MySQL 資料庫，我們可能會超出如何 toocomplete 某些基本工作。

首先，我們可以建立資料表並在其中載入一些資料。 我們將建立一個儲存清查資訊的資料表。
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>資料載入至 hello 資料表
既然我們已有資料表，我們可以在其中插入一些資料。 在 hello 開啟命令提示字元視窗中，請執行下列查詢 tooinsert hello 某些資料列的資料。
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

現在您有兩個資料列範例資料插入 hello 您稍早建立的資料表。

## <a name="query-and-update-hello-data-in-hello-tables"></a>查詢和更新 hello 資料表中的 hello 資料
執行 hello hello 資料庫資料表中的下列查詢 tooretrieve 資訊。
```sql
SELECT * FROM inventory;
```

您也可以更新 hello hello 資料表中的資料。
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

當您擷取資料時，取得據以更新 hello 資料列。
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>還原資料庫 tooa 前一個點的時間
想像您不小心刪除重要的資料庫資料表，並無法輕易復原 hello 資料。 Azure 的 MySQL 資料庫可讓您 toorestore hello 伺服器 tooa 點的時間，建立新的伺服器一個 hello 資料庫的副本。 您可以使用這個新的伺服器 toorecover 刪除的資料。 hello 加入 hello 資料表之前，請遵循步驟還原 hello 範例伺服器 tooa 點。

1. 在 hello Azure 入口網站，找出用於 MySQL 的 Azure 資料庫。 在 hello**概觀**頁面上，按一下**還原**hello 工具列上。 hello 還原頁面隨即開啟。

   ![10-1 還原資料庫](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. 填寫 hello**還原**hello 所需資訊的表單。
   
   ![10-2 還原表單](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **還原點**： 選取的時間點想 toorestore，列出的 hello 時間範圍內。 請確定 tooconvert 本地時區 tooUTC。
   - **還原 toonew 伺服器**： 提供新的伺服器名稱，您想要 toorestore。
   - **位置**: hello 區域與 hello 來源伺服器相同，且無法變更。
   - **定價層**: hello 定價層為的 hello hello 與相同來源伺服器，而且無法變更。
   
3. 按一下**確定**toorestore hello 伺服器太[還原時間點 tooa](./howto-restore-server-portal.md) hello 資料表已刪除之前。 還原伺服器建立一個新的 hello server，位於 hello 您指定的時間點複本。 

## <a name="next-steps"></a>後續步驟
在此教學課程中，您可以使用 hello Azure 入口網站 toolearned 如何以：

> [!div class="checklist"]
> * 建立適用於 MySQL 的 Azure 資料庫
> * Hello 伺服器防火牆設定
> * 使用 mysql 命令列工具 toocreate 資料庫
> * 載入範例資料
> * 查詢資料
> * 更新資料
> * 還原資料

> [!div class="nextstepaction"]
> [Tooconnect 應用程式 tooAzure 如何針對 MySQL 資料庫](./howto-connection-string.md)
