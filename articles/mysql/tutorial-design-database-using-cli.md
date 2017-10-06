---
title: "第一個 Azure 資料庫的 MySQL 資料庫-Azure CLI aaaDesign |Microsoft 文件"
description: "本教學課程說明如何 toocreate 和管理 Azure 資料庫的 MySQL 伺服器資料庫從 hello 命令列使用 Azure CLI 2.0。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>設計您第一個適用於 MySQL 資料庫的 Azure 資料庫

Azure 的 MySQL 資料庫是關聯式資料庫中的服務 hello Microsoft 雲端式 MySQL Community Edition 資料庫引擎上。 在此教學課程中，您使用 Azure CLI （命令列介面） 和其他公用程式 toolearn 如何以：

> [!div class="checklist"]
> * 建立適用於 MySQL 的 Azure 資料庫
> * Hello 伺服器防火牆設定
> * 使用[mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)toocreate 資料庫
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
使用 [az group create](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) 命令來建立 [Azure 資源群組](https://docs.microsoft.com/cli/azure/group#create)。 資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。

hello 下列範例會建立名為的資源群組`mycliresource`在 hello`westus`位置。

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>建立適用於 MySQL 的 Azure 資料庫伺服器
建立 Azure 資料庫的 MySQL 伺服器 hello az mysql 伺服器建立命令。 一部伺服器可以管理多個資料庫。 一般而言，每個專案或每個使用者會使用個別的資料庫。

hello 下列範例會建立 Azure 資料庫的 MySQL 伺服器位於`westus`hello 資源群組中`mycliresource`名稱`mycliserver`。 hello 伺服器具有系統管理員記錄檔中名為`myadmin`和密碼`Password01!`。 hello 伺服器會透過**基本**效能層和**50** hello 伺服器中的所有 hello 資料庫之間共用的單位。 您可以個別調整運算和儲存體向上或向下視 hello 應用程式需求而定。

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>設定防火牆規則
建立 Azure 資料庫與 hello az mysql 伺服器防火牆規則的 MySQL 伺服器層級防火牆規則建立命令。 伺服器層級防火牆規則允許外部應用程式，例如**mysql**命令列工具或 MySQL Workbench tooconnect tooyour 伺服器透過 hello Azure MySQL 服務防火牆。 

hello 下列範例會建立預先定義的位址範圍的防火牆規則。 此範例會顯示 hello 整個可能的 IP 位址範圍。

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>取得 hello 的連接資訊

tooconnect tooyour 伺服器，您需要 tooprovide 主機資訊和存取認證。
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

hello 結果是以 JSON 格式。 請記下 hello **fullyQualifiedDomainName**和**administratorLogin**。
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a>使用 mysql toohello 伺服器連接
使用[mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)tooestablish MySQL 伺服器的連線 tooyour Azure 資料庫。 在此範例中，hello 命令為：
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>建立空白資料庫
一旦您已連線的 toohello 伺服器，建立一個空白資料庫。
```sql
mysql> CREATE DATABASE mysampledb;
```

在 hello 提示字元中執行下列命令 tooswitch hello 連線 toothis 新建資料庫的 hello:
```sql
mysql> USE mysampledb;
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
想像一下您不小心刪除了這個資料表。 這是您無法輕易復原的情況。 Azure 的 MySQL 資料庫可讓您 toogo 後 tooany 點時間 hello 上次向上 too35 天並還原時間 tooa 新的伺服器中的這一點。 您可以使用這個新的伺服器 toorecover 刪除的資料。 hello 加入 hello 資料表之前，請遵循步驟還原 hello 範例伺服器 tooa 點。

Hello 還原您需要下列資訊的 hello:

- 還原點： 選取在時間點所發生之前 hello 伺服器已變更。 必須大於或等於 toohello 來源資料庫的最舊的備份值。
- 目標伺服器： 提供新的伺服器名稱，您想要 toorestore
- 來源伺服器： 提供您想要從 toorestore 的 hello 伺服器 hello 名稱
- 位置： 您無法選取 hello 區域，依預設它是與 hello 來源伺服器相同

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

toorestore hello 伺服器和[還原 tooa 時間點](./howto-restore-server-portal.md)hello 資料表已刪除之前。 還原伺服器 tooa 不同點時間建立重複的新伺服器與 hello 原始伺服器在您指定的時間點 hello，前提是它在 hello 的保留期限內是您[服務層](./concepts-service-tiers.md)。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已了解：
> [!div class="checklist"]
> * 建立適用於 MySQL 的 Azure 資料庫
> * Hello 伺服器防火牆設定
> * 使用[mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)toocreate 資料庫
> * 載入範例資料
> * 查詢資料
> * 更新資料
> * 還原資料

> [!div class="nextstepaction"]
> [適用於 MySQL 的 Azure 資料庫 - Azuer CLI 範例](./sample-scripts-azure-cli.md)
