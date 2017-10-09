---
title: "Azure PostgreSQL 資料庫中的 aaaConfigure hello 服務參數 |Microsoft 文件"
description: "本文說明如何 tooconfigure hello 服務在 Azure 資料庫使用於參數 PostgreSQL hello Azure CLI 命令列。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>使用 Azure CLI 自訂伺服器設定參數
您可以列出、 顯示及更新適用於使用命令列介面 (Azure CLI) hello Azure PostgreSQL 伺服器組態參數。 不過，只有一部分引擎設定會在伺服器層級公開而可供修改。 

## <a name="prerequisites"></a>必要條件
透過這個方式 tooguide toostep，您需要：
- 伺服器和資料庫 [建立適用於 PostgreSQL 的 Azure 資料庫](quickstart-create-server-database-azure-cli.md)
- 安裝[Azure CLI 2.0](/cli/azure/install-azure-cli)命令列公用程式或使用 hello Azure 雲端殼層 hello 瀏覽器中的。

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>列出適用於 PostgreSQL 伺服器之 Azure 資料庫的伺服器組態參數
toolist 中一部伺服器和其值，所有可修改的參數執行 hello [az postgres 伺服器組態清單](/cli/azure/postgres/server/configuration#list)命令。

您可以列出 hello 伺服器 hello 伺服器組態參數**mypgserver 20170401.postgres.database.azure.com**資源群組下**myresourcegroup**。
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>顯示伺服器設定參數的詳細資料
tooshow hello，執行的伺服器的特定組態參數的詳細資料[az postgres 伺服器組態顯示](/cli/azure/postgres/server/configuration#show)命令。

這個範例會顯示詳細資料的 hello**記錄\_min\_訊息**伺服器的伺服器組態參數**mypgserver 20170401.postgres.database.azure.com**下資源群組**myresourcegroup。**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>修改伺服器設定參數值
您也可以修改某些伺服器組態參數 hello 值，這會更新 hello PostgreSQL 伺服器引擎的 hello 基礎組態值。 tooupdate hello 組態使用 hello [az postgres 伺服器組態集](/cli/azure/postgres/server/configuration#set)命令。 

tooupdate hello**記錄\_min\_訊息**伺服器的伺服器組態參數**mypgserver 20170401.postgres.database.azure.com**資源群組下**myresourcegroup。**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
如果您想 tooreset hello 參數值的組態，您只需選擇出 hello 選擇性 tooleave`--value`參數和 hello 服務將會套用 hello 預設值。 在上述範例中，看起來應該像這樣：
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
這將會重設 hello**記錄\_min\_訊息**組態 toohello 預設值**警告**。 如需伺服器設定和允許值的進一步詳細資訊，請參閱有關[伺服器設定](https://www.postgresql.org/docs/9.6/static/runtime-config.html)的 PostgreSQL 文件。

## <a name="next-steps"></a>後續步驟
- tooconfigure 及存取伺服器記錄檔，請參閱[Azure PostgreSQL 資料庫中的伺服器記錄檔](concepts-server-logs.md)
