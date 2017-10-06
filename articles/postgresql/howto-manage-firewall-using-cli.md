---
title: "aaaCreate 及管理 Azure 資料庫使用 Azure CLI PostgreSQL 防火牆規則 |Microsoft 文件"
description: "本文說明如何 toocreate 及 PostgreSQL 防火牆規則，使用 Azure CLI 命令列管理 Azure 資料庫。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則
伺服器層級防火牆規則可讓系統管理員 toomanage 存取 tooan Azure Database PostgreSQL 伺服器從特定的 IP 位址或 IP 位址範圍。 您可以使用方便 Azure CLI 命令，來建立、 更新、 刪除、 清單，並顯示您的伺服器防火牆規則 toomanage。 如需「適用於 PostgreSQL 的 Azure 資料庫」防火牆的概觀，請參閱[適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則](concepts-firewall-rules.md)

## <a name="prerequisites"></a>必要條件
透過這個方式 tooguide toostep，您需要：
- [「適用於 PostgreSQL 的 Azure 資料庫」伺服器和資料庫](quickstart-create-server-database-azure-cli.md)
- 安裝[Azure CLI 2.0](/cli/azure/install-azure-cli)命令列公用程式或使用 hello Azure 雲端殼層 hello 瀏覽器中的。

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>設定「適用於 PostgreSQL 的 Azure 資料庫」的防火牆規則
hello [az postgres 伺服器防火牆規則](/cli/azure/postgres/server/firewall-rule)命令會使用的 tooconfigure 防火牆規則。

## <a name="list-firewall-rules"></a>列出防火牆規則 
toolist hello 現有伺服器防火牆規則 hello 在伺服器上，執行 hello [az postgres 伺服器防火牆規則清單](/cli/azure/postgres/server/firewall-rule#list)命令。
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
如果依預設，在 JSON 中的任何格式，hello 輸出會列出 hello 規則。 您可以使用 hello 交換器`--output table`更容易閱讀的表格格式做為 hello 輸出。
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>建立防火牆規則
新的防火牆規則 hello 在伺服器上，執行 hello toocreate [az postgres 伺服器防火牆規則建立](/cli/azure/postgres/server/firewall-rule#create)命令。 

這個範例允許所有 IP 位址 tooaccess hello 伺服器範圍**mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
tooallow 單數的 IP 位址 tooaccess，提供 hello 起始 IP 和結束 IP，如此範例所示為 hello 相同的位址。
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
成功時，hello 命令輸出會列出您已建立，根據預設，在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。 如果失敗，hello 改為輸出 showserror 訊息文字。

## <a name="update-firewall-rule"></a>更新防火牆規則 
更新現有防火牆規則上 hello 伺服器使用[az postgres 伺服器防火牆規則更新](/cli/azure/postgres/server/firewall-rule#update)命令。 提供 hello 做為輸入，而且 hello 起始 IP 和結束 IP 屬性 tooupdate hello 現有防火牆規則名稱。
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
成功時，hello 命令輸出會列出您已更新，根據預設，在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。 如果失敗，hello 改為輸出 showserror 訊息文字。
> [!NOTE]
> 如果 hello 防火牆規則不存在，它取得建立 hello 更新命令。

## <a name="show-firewall-rule-details"></a>顯示防火牆規則詳細資料
您也可以顯示 hello 現有防火牆規則的詳細資料的伺服器執行[az postgres 伺服器防火牆規則顯示](/cli/azure/postgres/server/firewall-rule#show)命令。
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
成功時，hello 命令輸出會列出您已指定，預設會在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。 如果失敗，hello 改為輸出 showserror 訊息文字。

## <a name="delete-firewall-rule"></a>刪除防火牆規則
IP 範圍從 hello 伺服器 toorevoke 存取刪除現有的防火牆規則執行 hello [az postgres 伺服器防火牆規則刪除](/cli/azure/postgres/server/firewall-rule#delete)命令。 提供 hello hello 現有防火牆規則名稱。
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
成功時，沒有任何輸出。 在發生錯誤時，會傳回 hello 錯誤訊息文字。

## <a name="next-steps"></a>後續步驟
- 同樣地，您可以使用網頁瀏覽器太[建立及管理 Azure 資料庫使用 hello Azure 入口網站的 PostgreSQL 防火牆規則](howto-manage-firewall-using-portal.md)
- 進一步了解[適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則](concepts-firewall-rules.md)
- 連線 PostgreSQL 伺服器 tooan Azure 資料庫的說明，請參閱[PostgreSQL 的 Azure 資料庫的連接程式庫](concepts-connection-libraries.md)
