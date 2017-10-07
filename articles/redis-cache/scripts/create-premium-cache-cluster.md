---
title: "aaaAzure CLI 指令碼範例-建立 Premium Azure Redis 快取叢集 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立具有叢集的 Premium 層 Azure Redis 快取"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a>建立具有叢集的 Premium Azure Redis 快取

在此案例中，您將學會如何 toocreate 6 GB Premium 層 Azure Redis 快取叢集啟用和兩個分區。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 資源群組和 Premium 層 redis 快取叢集啟用。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az redis create](https://docs.microsoft.com/cli/azure/redis#create) | 建立 Redis 快取執行個體。 |


## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他的 Azure Redis 快取 CLI 指令碼範例可以在 hello [Azure Redis 快取文件](../cli-samples.md)。
