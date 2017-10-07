---
title: "aaaCLI 範例調整 SQL 彈性集區-Azure SQL 資料庫 |Microsoft 文件"
description: "Azure CLI 範例指令碼 tooscale Azure SQL Database 中的 SQL 彈性集區"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a>使用 CLI tooscale Azure SQL Database 中的 SQL 彈性集區

此 Azure CLI 指令碼範例會建立 SQL 彈性集區、移動集區資料庫，以及變更彈性集區的效能等級。 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>清除部署

Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組中，邏輯伺服器，SQL Database 和防火牆規則的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | 建立主機 hello SQL Database 邏輯伺服器。 |
| [az sql elastic-pools create](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | 建立 hello 邏輯伺服器內的彈性資料庫集區。 |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#create) | 建立 hello 邏輯伺服器中的 hello SQL 資料庫。 |
| [az sql elastic-pools update](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | 更新的彈性資料庫集區，在此範例變更 hello 分派 eDTU。 |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他的 SQL 資料庫 CLI 指令碼範例可以在 hello [Azure SQL Database 文件](../sql-database-cli-samples.md)。
