---
title: "aaaCLI 範例建立 Azure SQL database |Microsoft 文件"
description: "Azure CLI 範例指令碼 toocreate SQL 資料庫"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a>使用 CLI toocreate 單一 Azure SQL 資料庫並設定防火牆規則

此 CLI 指令碼範例會建立 Azure SQL Database 並設定伺服器層級防火牆規則。 一旦 hello 指令碼順利執行之後，您可以從所有 Azure 服務存取 SQL Database 的 hello 與 hello 設定 IP 位址。 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a>清除部署

Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az sql server create](/cli/azure/sql/server#create) | 建立主機 hello SQL Database 邏輯伺服器。 |
| [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) | Hello hello 輸入 IP 位址範圍內的伺服器上建立防火牆規則 tooallow 存取 tooall SQL 資料庫。 |
| [az sql db create](/cli/azure/sql/db#create) | 建立 hello 邏輯伺服器中的 hello SQL 資料庫。 |
| [az group delete](/cli/azure/resource#delete) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他的 SQL 資料庫 CLI 指令碼範例可以在 hello [Azure SQL Database 文件](../sql-database-cli-samples.md)。

