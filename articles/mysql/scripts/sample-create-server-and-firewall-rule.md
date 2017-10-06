---
title: "aaa\"Azure CLI 指令碼-建立 Azure 的資料庫，MySQL |Microsoft 文件 」"
description: "此範例 CLI 指令碼會建立「適用於 MySQL 的 Azure 資料庫」伺服器，並設定伺服器等級防火牆規則。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>建立 MySQL 伺服器及設定使用 Azure CLI hello 的防火牆規則
此範例 CLI 指令碼會建立「適用於 MySQL 的 Azure 資料庫」伺服器，並設定伺服器等級防火牆規則。 一旦 hello 指令碼順利執行，hello MySQL 伺服器可供所有 Azure 服務存取，而且 hello 設定 IP 位址。

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="sample-script"></a>範例指令碼
在這個範例指令碼中，編輯 hello 反白顯示線條 toocustomize hello 管理員使用者名稱和密碼。
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>清除部署
Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>指令碼說明
此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| **命令** | **注意事項** |
|---|---|
| [az group create](/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az mysql server create](/cli/azure/mysql/server#create) | 建立裝載 hello 資料庫的 MySQL 伺服器。 |
| [az mysql server firewall create](/cli/azure/mysql/server/firewall-rule#create) | 來自 hello 輸入 IP 位址範圍建立防火牆規則 tooallow 存取 toohello 伺服器和其下的資料庫。 |
| [az group delete](/cli/azure/group#delete) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟
- 閱讀更多有關 hello Azure CLI: [Azure CLI 文件](/cli/azure/overview)。
- 嘗試其他指令碼：[「適用於 MySQL 的 Azure 資料庫」的 Azure CLI 範例](../sample-scripts-azure-cli.md)
