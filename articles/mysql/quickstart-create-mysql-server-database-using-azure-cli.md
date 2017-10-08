---
title: "快速入門：建立 Azure Database for MySQL 伺服器 - Azuer CLI | Microsoft Docs"
description: "本快速入門說明如何 toouse 會 hello Azure CLI toocreate Azure 資源群組中的 MySQL server Azure 資料庫。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>使用 Azure CLI 建立 Azure Database for MySQL 伺服器
本快速入門說明如何 toouse hello Azure CLI toocreate Azure 資源群組中的 MySQL server Azure 資料庫在五分鐘內。 hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。

如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

如果您有多個訂閱，選擇適當 hello 訂閱 hello 資源存在或已支付。 使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>建立資源群組
建立[Azure 資源群組](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)使用 hello [az 群組建立](https://docs.microsoft.com/cli/azure/group#create)命令。 資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。

hello 下列範例會建立名為的資源群組`myresourcegroup`在 hello`westus`位置。

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>建立適用於 MySQL 的 Azure 資料庫伺服器
建立 MySQL 伺服器的 Azure 資料庫以 hello **az mysql 伺服器建立**命令。 一部伺服器可以管理多個資料庫。 一般而言，每個專案或每個使用者會使用個別的資料庫。

hello 下列範例會建立 Azure 資料庫的 MySQL 伺服器位於`westus`hello 資源群組中`myresourcegroup`名稱`myserver4demo`。 hello 伺服器具有系統管理員記錄檔中名為`myadmin`和密碼`Password01!`。 hello 伺服器會透過**基本**效能層和**50** hello 伺服器中的所有 hello 資料庫之間共用的單位。 您可以個別調整運算和儲存體向上或向下視 hello 應用程式需求而定。

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>設定防火牆規則
建立 Azure 資料庫的 MySQL 伺服器層級防火牆規則使用 hello **az mysql 伺服器防火牆規則建立**命令。 伺服器層級防火牆規則可讓外部應用程式，例如 hello **mysql.exe**命令列工具或 MySQL Workbench tooconnect tooyour 伺服器透過 hello Azure MySQL 服務防火牆。 

hello 下列範例會建立的預先定義的位址範圍，在此範例中是 hello 整個可能的 IP 位址範圍的防火牆規則。

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>進行 SSL 設定
預設會強制執行您的伺服器與用戶端應用程式之間的 SSL 連線。  這可確保安全性的 「 移動 」 透過加密 hello 資料流資料 hello 網際網路。  此快速入門更容易 toomake，我們停用您伺服器的 SSL 連線。  不建議對生產伺服器這麼做。  如需詳細資訊，請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](./howto-configure-ssl.md)。

hello 下列範例會停用強制執行您的 MySQL 伺服器上的 SSL。
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>取得 hello 的連接資訊

tooconnect tooyour 伺服器，您需要 tooprovide 主機資訊和存取認證。

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

hello 結果是以 JSON 格式。 請記下 hello **fullyQualifiedDomainName**和**administratorLogin**。
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>使用命令列工具的 hello mysql.exe toohello 伺服器連接
使用 hello tooyour 伺服器連接**mysql.exe**命令列工具。 您可以從[這裡](https://dev.mysql.com/downloads/)下載 MySQL，再將它安裝於電腦上。 而您也可以按一下 hello**試試**程式碼範例，按鈕或 hello`>_`按鈕 hello 上方右側的工具列中 hello Azure 入口網站，並啟動 hello **Azure 雲端殼層**。

輸入 hello 下一個命令： 

1. 連接伺服器所使用的 toohello **mysql**命令列工具：
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. 檢視伺服器狀態：
```sql
 mysql> status
```
如果一切順利，hello 命令列工具應該輸出 hello 下列文字：

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> 如需其他命令，請參閱 [MySQL 5.7 參考手冊 - 第 4.5.1 章](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)。

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>使用 hello MySQL Workbench GUI 工具 toohello 伺服器連接
1.  啟動 hello MySQL Workbench 用戶端電腦上的應用程式。 您可以從[這裡](https://dev.mysql.com/downloads/workbench/)下載並安裝 MySQL Workbench。

2.  在 [hello**設定新連線**對話方塊方塊中，輸入下列資訊 hello**參數**] 索引標籤：

   ![設定新連線](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **設定** | **建議的值** | **說明** |
|---|---|---|
|   連線名稱 | 我的連線 | 指定此連線的標籤 (這可以是任何項目) |
| 連線方式 | 選擇標準 (TCP/IP) | 用於 MySQL 的 TCP/IP 通訊協定 tooconnect tooAzure 資料庫 > |
| 主機名稱 | myserver4demo.mysql.database.azure.com | 您先前記下的伺服器名稱。 |
| 連接埠 | 3306 | 會使用 MySQL 的 hello 預設通訊埠。 |
| 使用者名稱 | myadmin@myserver4demo | hello server 系統管理員登入您先前所述。 |
| 密碼 | **** | 使用您先前設定的 hello 系統管理員帳戶密碼。 |

按一下**測試連接**tootest 如果已正確設定所有參數。
現在，您可以按一下 hello 連接 toosuccessfully toohello 伺服器連接。

## <a name="clean-up-resources"></a>清除資源
如果您不需要這些資源，另一個快速入門/教學課程中，您可以刪除它們，執行下列命令的 hello: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 Azure CLI 設計 MySQL 資料庫](./tutorial-design-database-using-cli.md)
