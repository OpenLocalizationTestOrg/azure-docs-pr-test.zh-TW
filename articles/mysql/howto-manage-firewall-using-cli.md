---
title: "aaaCreate 和管理 Azure 資料庫的 MySQL 防火牆規則，使用 Azure CLI |Microsoft 文件"
description: "本文說明如何 toocreate 和 MySQL 防火牆規則，使用 Azure CLI 命令列管理 Azure 資料庫。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>使用 Azure CLI 建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則
伺服器層級防火牆規則可讓系統管理員 toomanage 存取 tooan Azure 資料庫的 MySQL 伺服器從特定的 IP 位址或 IP 位址範圍。 您可以使用方便 Azure CLI 命令，來建立、 更新、 刪除、 清單，並顯示您的伺服器防火牆規則 toomanage。 如需「適用於 MySQL 的 Azure 資料庫」防火牆的概觀，請參閱[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)

## <a name="prerequisites"></a>必要條件
* [安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* 安裝適用於 PostgreSQL 和 MySQL 服務的 Azure Python SDK
* 安裝 PostgreSQL 和 MySQL 服務的 hello Azure CLI 元件
* 建立適用於 MySQL 的 Azure 資料庫伺服器

## <a name="firewall-rule-commands"></a>防火牆規則的命令︰
hello **az mysql 伺服器防火牆規則**命令用來從 Azure CLI toocreate、 刪除、 清單、 顯示，並更新防火牆規則。

命令：
- **create**︰建立 Azure MySQL 伺服器防火牆規則。
- **delete**︰刪除 Azure MySQL 伺服器防火牆規則。
- **清單**: hello Azure MySQL 伺服器防火牆規則的清單。
- **顯示**： 顯示 hello 詳細資料，Azure MySQL 伺服器的防火牆規則。
- **update**：更新 Azure MySQL 伺服器防火牆規則。

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>登入 tooAzure 和清單 Azure 資料庫的 MySQL 伺服器
安全地連線 Azure CLI 與 Azure 帳戶。 使用 hello **az 登入**toodo 這樣的命令。

1. 執行 hello hello 命令列中的下列命令。
```azurecli
az login
```
此命令會輸出的程式碼 toouse hello 下一個步驟中。

2. 使用網頁瀏覽器 tooopen hello 頁面[https://aka.ms/devicelogin](https://aka.ms/devicelogin)輸入 hello 程式碼。

3. 在 hello 提示字元中使用登入您的 Azure 認證。

4. 一旦您的登入已獲得授權，將會列印 hello 主控台的訂閱清單。 複製 hello 識別碼 hello 的所需的訂用帳戶 tooset hello 目前訂用帳戶 toobe 使用向前移動。
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. 如果您不確定的 hello 名稱，清單為您的訂用帳戶和資源群組的 MySQL 伺服器 hello Azure 資料庫。

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   請注意 hello 中的 name 屬性，藉以 hello 會使用的 toospecify 上的 MySQL server toowork。 如果需要請確認該伺服器 toousing hello 屬性 tooconfirm 名稱是正確的 hello 詳細資料：

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>在「適用於 MySQL 的 Azure 資料庫」伺服器上列出防火牆規則 
使用 hello 伺服器名稱和 hello 資源群組名稱，此清單 hello 現有伺服器上的防火牆規則 hello 伺服器。 請注意該 hello server name 屬性會指定在 hello **-伺服器**切換並不 hello **-名稱**切換。
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
如果依預設，在 JSON 中的任何格式，hello 輸出會列出 hello 規則。 您可以使用 hello 交換器**-輸出資料表**更容易閱讀的表格格式做為 hello 輸出。
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>在「適用於 MySQL 的 Azure 資料庫」伺服器上建立防火牆規則
使用 hello Azure MySQL 伺服器名稱和 hello 資源群組名稱，hello 伺服器上建立新的防火牆規則。 提供 hello 規則 toocover 範圍的 IP 位址 tooallow 存取 hello 規則、 hello 開始 IP 和結束 IP 的名稱。
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
單數的 ip 位址 toobe 允許存取，請提供 hello 起始 IP 和結束 IP，如此範例所示為 hello 相同的位址。
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
成功時，hello 命令輸出會列出您已建立，根據預設，在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。 如果失敗，hello 輸出就會改為顯示錯誤訊息文字。

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>在「適用於 MySQL 的 Azure 資料庫」伺服器上更新防火牆規則 
使用 hello Azure MySQL 伺服器名稱和 hello 資源群組名稱，更新現有防火牆規則 hello 伺服器上。 提供 hello 做為輸入，而且 hello 起始 IP 和結束 IP 屬性 tooupdate hello 現有防火牆規則名稱。
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
成功時，hello 命令輸出會列出您已更新，根據預設，在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。 如果失敗，hello 輸出就會改為顯示錯誤訊息文字。

> [!NOTE]
> 如果 hello 防火牆規則不存在，它將會建立 hello 更新命令。

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>在「適用於 MySQL 的 Azure 資料庫」伺服器上顯示防火牆規則詳細資料
使用 hello Azure MySQL 伺服器名稱和 hello 資源群組名稱，顯示 hello 現有防火牆規則詳細資料從伺服器 hello。 提供 hello hello 現有防火牆規則名稱做為輸入。
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
成功時，hello 命令輸出會列出您已指定，預設會在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。 如果失敗，hello 輸出就會改為顯示錯誤訊息文字。

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>在「適用於 MySQL 的 Azure 資料庫」伺服器上刪除防火牆規則
使用 hello Azure MySQL 伺服器名稱和 hello 資源群組名稱，從 hello 伺服器移除現有的防火牆規則。 提供 hello hello 現有防火牆規則名稱。
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
成功時，沒有任何輸出。 在發生錯誤時，將會傳回 hello 錯誤訊息文字。

## <a name="next-steps"></a>後續步驟
- 進一步了解[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)
- [建立和管理 Azure 資料庫的 MySQL 使用 hello Azure 入口網站的防火牆規則](./howto-manage-firewall-using-portal.md)
