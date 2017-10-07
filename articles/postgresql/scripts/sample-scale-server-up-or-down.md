---
title: "aaa\"Azure CLI 指令碼標尺 Azure PostgreSQL 資料庫 |Microsoft 文件 」"
description: "Azure CLI 指令碼範例-PostgreSQL 伺服器 tooa 不同效能層級之後查詢 hello 度量的小數位數 Azure 資料庫。"
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>使用 Azure CLI 監視和調整單一 PostgreSQL 伺服器
這個範例 CLI 指令碼之後查詢 hello 度量縮放單一 Azure 資料庫 PostgreSQL 伺服器 tooa 不同的效能層級。 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="sample-script"></a>範例指令碼
在這個範例指令碼中，變更反白顯示 hello 行 toocustomize hello 管理員使用者名稱和密碼。 取代您自己的訂用帳戶 id 與 hello az 監視器命令中使用的 hello 訂用帳戶 id。[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>清除部署
Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>指令碼說明
此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| **命令** | **注意事項** |
|---|---|
| [az group create](/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az postgres server create](/cli/azure/postgres/server#create) | 建立 PostgreSQL 伺服器主控 hello 資料庫。 |
| [az monitor metrics list](/cli/azure/monitor/metrics#list) | 列出 hello 資源 hello 公制值。 |
| [az group delete](/cli/azure/group#delete) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟
- 閱讀更多有關 hello Azure CLI: [Azure CLI 文件](/cli/azure/overview)
- 嘗試其他指令碼：[「適用於 PostgreSQL 的 Azure 資料庫」的 Azure CLI 範例](../sample-scripts-azure-cli.md)
- 了解調整的詳細資訊：[服務層](../concepts-service-tiers.md)及[計算單位和儲存單位](../concepts-compute-unit-and-storage.md)
