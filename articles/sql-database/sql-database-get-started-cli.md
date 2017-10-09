---
title: "Azure CLI：建立 SQL Database | Microsoft Docs"
description: "了解 toocreate SQL Database 邏輯伺服器，伺服器層級防火牆規則，並使用資料庫 hello Azure CLI。"
keywords: "sql database 教學課程, 建立 sql database"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>建立單一的 Azure SQL database，使用 Azure CLI hello

hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。 此指南使用 hello Azure CLI toodeploy 詳細資料中的 Azure SQL database [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)中[Azure SQL Database 邏輯伺服器](sql-database-features.md)。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，這個主題需要執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="define-variables"></a>定義變數

在這個快速入門中的 hello 指令碼中定義使用的變數。

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>建立資源群組

建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)使用 hello [az 群組建立](/cli/azure/group#create)命令。 資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。 hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westeurope`位置。

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>建立邏輯伺服器

建立[Azure SQL Database 邏輯伺服器](sql-database-features.md)使用 hello [az sql server 建立](/cli/azure/sql/server#create)命令。 邏輯伺服器包含一組當作群組管理的資料庫。 hello 下列範例會建立隨機命名的伺服器資源群組中具有系統管理員登入名為`ServerAdmin`且密碼為`ChangeYourAdminPassword1`。 視需要取代這些預先定義的值。

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>設定伺服器防火牆規則

建立[Azure SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)使用 hello [az sql server 防火牆建立](/cli/azure/sql/server/firewall-rule#create)命令。 伺服器層級防火牆規則可讓外部應用程式，例如 SQL Server Management Studio 或 hello SQLCMD 公用程式 tooconnect tooa SQL database 透過 hello SQL Database 服務防火牆。 在下列範例的 hello，hello 開啟防火牆會僅針對其他 Azure 資源。 tooenable 外部連線，變更 hello IP 位址 tooan 適當的位址，為您的環境。 tooopen 所有 IP 位址，都作為 hello 起始 IP 位址和 255.255.255.255 hello 結束位址為 0.0.0.0。  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> SQL Database 會透過連接埠 1433 通訊。 如果您嘗試 tooconnect 從公司網路內，由您的網路防火牆可能不允許透過通訊埠 1433年的輸出流量。 如果是的話，就能 tooconnect tooyour Azure SQL Database 伺服器除非您的 IT 部門會開啟通訊埠 1433年。
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>以範例資料的 hello 伺服器中建立資料庫

建立與資料庫[S0 的效能層級](sql-database-service-tiers.md)hello 伺服器使用 hello [az sql 資料庫建立](/cli/azure/sql/db#create)命令。 hello 下列範例會建立一個稱為資料庫`mySampleDatabase`和載入 hello 有提供 AdventureWorksLT 範例資料到此資料庫。 這些預先定義的取代值，則為所需 （在這個快速入門中的 hello 值的這個集合組建中其他快速開始）。

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>清除資源

此集合中的其他快速入門會建置在本快速入門。 

> [!TIP]
> 如果您計劃 toocontinue toowork 與後續的快速入門，請不要清除 hello 資源建立在這個快速開始。 如果您不打算 toocontinue，使用 hello 本快速入門 hello Azure 入口網站中的下列步驟 toodelete 建立所有資源。
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>後續步驟

您現在具有資料庫，您可使用最愛的工具進行連線和查詢。 選擇下列工具來深入了解︰

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

