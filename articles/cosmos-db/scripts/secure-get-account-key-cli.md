---
title: "Azure CLI 指令碼 - 取得 Azure Cosmos DB 的帳戶金鑰 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 取得 Azure Cosmos DB 的帳戶金鑰"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 3df211cdc8878033c8b792da00cce9773ae57a36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-the-azure-cli"></a>使用 Azure CLI 取得 Azure Cosmos DB 的帳戶金鑰

這個範例會取得任何一種 Azure Cosmos DB 帳戶的帳戶金鑰。  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。 執行 `az --version` 以尋找版本。 如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[主要](../../../cli_scripts/cosmosdb/scale-cosmosdb-get-account-key/secure-cosmosdb-get-account-key.sh?highlight=22-25 "取得 Azure Cosmos DB 帳戶金鑰")]

## <a name="clean-up-deployment"></a>清除部署

在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令。 下表中的每個命令都會連結至命令特定的文件。

| 命令 | 注意事項 |
|---|---|
| [az group create](/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az cosmosdb update](https://docs.microsoft.com/cli/azure/cosmosdb#update) | 更新 Azure Cosmos DB 帳戶。 |
| [az cosmosdb list-keys](https://docs.microsoft.com/cli/azure/cosmosdb#list-keys) | 建立主控 SQL Database 的邏輯伺服器。 |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以在 [Azure Cosmos DB CLI 文件](../cli-samples.md)中找到其他 Azure Cosmos DB CLI 指令碼範例。