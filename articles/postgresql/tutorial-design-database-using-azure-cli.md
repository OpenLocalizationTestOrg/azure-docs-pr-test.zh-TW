---
title: "使用 Azure CLI 來設計您第一個適用於 PostgreSQL 的 Azure 資料庫 | Microsoft Docs"
description: "本教學課程示範如何 tooDesign 第一次 Azure 資料庫，以獲得 PostgreSQL 使用 Azure CLI。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>使用 Azure CLI 來設計您第一個適用於 PostgreSQL 的 Azure 資料庫 
在此教學課程中，您使用 Azure CLI （命令列介面） 和其他公用程式 toolearn 如何以：
> [!div class="checklist"]
> * 建立適用於 PostgreSQL 的 Azure 資料庫
> * Hello 伺服器防火牆設定
> * 使用[ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html)公用程式 toocreate 資料庫
> * 載入範例資料
> * 查詢資料
> * 更新資料
> * 還原資料

您可以使用在 hello 瀏覽器中的 hello Azure 雲端殼層或[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)在本教學課程中您自己電腦 toorun hello 程式碼區塊。

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

如果您有多個訂閱，選擇適當 hello 訂閱 hello 資源存在或已支付。 使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>建立資源群組
建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)使用 hello [az 群組建立](/cli/azure/group#create)命令。 資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。 hello 下列範例會建立名為的資源群組`myresourcegroup`在 hello`westus`位置。
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>建立適用於 PostgreSQL 的 Azure 資料庫伺服器
建立[PostgreSQL server 的 Azure 資料庫](overview.md)使用 hello [az postgres 伺服器建立](/cli/azure/postgres/server#create)命令。 一個伺服器會包含一組以群組方式管理的資料庫。 

hello 下列範例會建立名為伺服器`mypgserver-20170401`資源群組中`myresourcegroup`與伺服器系統管理員登入`mylogin`。 伺服器的名稱將 tooDNS 名稱對應，因此在 Azure 中全域唯一的必要的 toobe。 替代 hello`<server_admin_password>`與您自己的值。
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> hello 伺服器系統管理員登入和密碼，您在此處指定為 toohello server 中的必要的 toolog 和其資料庫，稍後在這個快速入門。 請記住或記錄此資訊，以供稍後使用。

根據預設，**postgres** 資料庫會建立在您的伺服器底下。 hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html)資料庫是適用於由使用者、 公用程式及協力廠商應用程式的預設資料庫。 


## <a name="configure-a-server-level-firewall-rule"></a>設定伺服器層級防火牆規則

建立 Azure PostgreSQL 伺服器層級防火牆規則以 hello [az postgres 伺服器防火牆規則建立](/cli/azure/postgres/server/firewall-rule#create)命令。 伺服器層級防火牆規則允許外部應用程式，例如[psql](https://www.postgresql.org/docs/9.2/static/app-psql.html)或[PgAdmin](https://www.pgadmin.org/) tooconnect tooyour 伺服器透過 hello Azure PostgreSQL 服務防火牆。 

您可以設定防火牆規則，它涵蓋了 IP 範圍 toobe 無法 tooconnect 從您的網路。 hello 下列範例會使用[az postgres 伺服器防火牆規則建立](/cli/azure/postgres/server/firewall-rule#create)toocreate 防火牆規則`AllowAllIps`ip 位址範圍。 tooopen 所有 IP 位址，都作為 hello 起始 IP 位址和 255.255.255.255 hello 結束位址為 0.0.0.0。
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure PostgreSQL 伺服器會透過連接埠 5432 進行通訊。 當您從公司網路內進行連線時，網路的防火牆可能不允許透過連接埠 5432 的輸出流量。 具有您開啟通訊埠 5432 tooconnect tooyour Azure SQL Database 伺服器的 IT 部門。
>

## <a name="get-hello-connection-information"></a>取得 hello 的連接資訊

tooconnect tooyour 伺服器，您需要 tooprovide 主機資訊和存取認證。
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

hello 結果是以 JSON 格式。 請記下 hello **administratorLogin**和**fullyQualifiedDomainName**。
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>連接 tooAzure 資料庫使用 psql PostgreSQL 資料庫
如果您的用戶端電腦已安裝的 PostgreSQL，您可以使用的本機執行個體[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html)，或 hello Azure 雲端主控台 tooconnect tooan Azure PostgreSQL 伺服器。 我們現在使用 hello psql 命令列公用程式 tooconnect toohello Azure Database PostgreSQL 伺服器。

1. 執行下列 psql 命令 tooconnect tooan Azure Database PostgreSQL 伺服器 hello
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  比方說，下列命令的 hello 連接 toohello 預設資料庫呼叫**postgres** PostgreSQL 伺服器上**mypgserver 20170401.postgres.database.azure.com**使用存取認證。 輸入 hello`<server_admin_password>`您選擇當系統提示您輸入密碼。
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  一旦您已連線的 toohello 伺服器，建立一個空白資料庫在 hello 提示字元。
```sql
CREATE DATABASE mypgsqldb;
```

3.  在 hello 提示字元中執行下列命令 tooswitch 連線 toohello 新建資料庫的 hello **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Hello 資料庫中建立資料表
您現在知道如何 tooconnect toohello PostgreSQL 的 Azure 資料庫，我們可能會超出如何 toocomplete 某些基本工作。

首先，我們可以建立資料表並在其中載入一些資料。 我們將建立一個追蹤清查資訊的資料表。
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

您可以看到新建立的資料表中的資料表的 hello 清單現在輸入 hello:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>資料載入至 hello 資料表
既然我們已有資料表，我們可以在其中插入一些資料。 在 hello 開啟命令提示字元視窗中，執行下列查詢 tooinsert hello 某些資料列的資料
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

您有範例資料插入您稍早建立的 hello 資料表現在包含兩個資料列。

## <a name="query-and-update-hello-data-in-hello-tables"></a>查詢和更新 hello 資料表中的 hello 資料
執行 hello hello 資料庫資料表中的下列查詢 tooretrieve 資訊。 
```sql
SELECT * FROM inventory;
```

您也可以更新 hello 資料表中的 hello 資料
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

當您擷取資料時，取得據以更新 hello 資料列。
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>還原資料庫 tooa 前一個點的時間
假設您不小心刪除了資料表。 這是您無法輕易復原的情況。 Azure PostgreSQL 資料庫可讓您 （在最後一個向上 too7 天 （基本） 則為 35 天 （標準） hello) 的 toogo 後 tooany 在時間點，並還原這個時間點 tooa 新的伺服器。 您可以使用這個新的伺服器 toorecover 刪除的資料。 hello 加入 hello 資料表之前，請遵循步驟還原 hello 範例伺服器 tooa 點。

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

hello`az postgres server restore`命令需要 hello 下列參數：
| 設定 | 建議的值 | 說明  |
| --- | --- | --- |
| --resource-group |  myResourceGroup |  資源群組中的 hello 來源伺服器已存在。  |
| --name | mypgserver-restored | hello hello hello restore 命令所建立的新伺服器名稱。 |
| restore-point-in-time | 2017-04-13T13:59:00Z | 選取以時間點 toorestore。 這個日期和時間必須在 hello 來源伺服器的備份保留期限內。 請使用 ISO8601 日期和時間格式。 例如，您可能會使用您自己的本地時區，例如 `2017-04-13T05:59:00-08:00`，或使用 UTC Zulu 格式 `2017-04-13T13:59:00Z`。 |
| --source-server | mypgserver-20170401 | hello 名稱或識別碼 hello 來源伺服器 toorestore 從。 |

還原伺服器 tooa 在時間點建立新的伺服器，做為 hello 原始伺服器 hello 點複製指定的時間。 hello 位置及定價層 hello 還原伺服器的值為 hello 與 hello 來源伺服器相同。

hello 命令為同步，而且將 hello 伺服器恢復正常後傳回。 一旦 hello 還原完成時，找出 hello 已建立的新伺服器。 請確認資料已還原，如預期般的 hello。


## <a name="next-steps"></a>後續步驟
在本教學課程中，您學到如何 toouse Azure CLI （命令列介面） 和其他公用程式：
> [!div class="checklist"]
> * 建立適用於 PostgreSQL 的 Azure 資料庫
> * Hello 伺服器防火牆設定
> * 使用[ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html)公用程式 toocreate 資料庫
> * 載入範例資料
> * 查詢資料
> * 更新資料
> * 還原資料

接下來，了解如何 toouse hello Azure 入口網站 toodo 類似的工作，請檢閱本教學課程： [PostgreSQL 使用 hello Azure 入口網站的設計您的第一個 Azure 資料庫](tutorial-design-database-using-azure-portal.md)
