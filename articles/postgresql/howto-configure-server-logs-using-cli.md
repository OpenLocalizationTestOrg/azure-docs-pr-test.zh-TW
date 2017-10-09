---
title: "使用 Azure CLI PostgreSQL 的 aaaConfigure 及存取伺服器記錄檔 |Microsoft 文件"
description: "本文說明如何 tooconfigure 及存取 hello 伺服器記錄檔中 Azure Database PostgreSQL 使用 Azure CLI 命令列。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>使用 Azure CLI 設定和存取伺服器記錄
您可以下載 hello PostgreSQL server 錯誤記錄檔使用 hello 命令列介面 (Azure CLI)。 不過，不支援存取 tootransaction 記錄檔。 

## <a name="prerequisites"></a>必要條件
透過這個方式 tooguide toostep，您需要：
- [適用於 PostgreSQL 的 Azure 資料庫伺服器](quickstart-create-server-database-azure-cli.md)
- 安裝[Azure CLI 2.0](/cli/azure/install-azure-cli)命令列公用程式或使用 hello Azure 雲端殼層 hello 瀏覽器中的。

## <a name="configure-logging-for-azure-database-for-postgresql"></a>設定「適用於 PostgreSQL 的 Azure 資料庫」的記錄
您可以設定 hello 伺服器 tooaccess 查詢記錄檔和錯誤記錄檔。 錯誤記錄可包含自動清空、連線和檢查點資訊。
1. 開啟記錄功能
2. 更新記錄\_陳述式和記錄\_min\_持續時間\_陳述式 tooenable 查詢記錄
3. 更新保留期限

如需詳細資訊，請參閱[自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)。

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>列出適用於 PostgreSQL 伺服器的 Azure 資料庫之記錄
toolist hello 可用的記錄檔以取得您的伺服器上執行 hello [az postgres 伺服器記錄檔清單](/cli/azure/postgres/server-logs#list)命令。

您可以列出 hello 記錄檔以取得伺服器**mypgserver 20170401.postgres.database.azure.com**資源群組下**myresourcegroup**，指示它 tooa 文字和名為檔案**記錄\_檔案\_list.txt。**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>從 hello 伺服器在本機下載記錄檔
hello [az postgres 伺服器記錄檔下載](/cli/azure/postgres/server-logs#download)命令可讓您 toodownload 個別記錄檔，為您的伺服器。 

此範例中下載 hello hello 伺服器的特定記錄檔**mypgserver 20170401.postgres.database.azure.com**資源群組下**myresourcegroup** tooyour 本機環境。
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>後續步驟
- toolearn 進一步了解伺服器記錄檔，請參閱[Azure PostgreSQL 資料庫中的伺服器記錄檔](concepts-server-logs.md)
- 如需伺服器參數的詳細資訊，請參閱[使用 Azure CLI 自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)
