---
title: "CLI 指令碼範例-取得 hello 主機名稱、 通訊埠，以及 Azure Redis 快取的索引鍵 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例-取得 hello 主機名稱、 通訊埠，以及 Azure Redis 快取執行個體的金鑰"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Azure Redis 快取中取得 hello 主機名稱、 通訊埠，以及索引鍵

在此案例中，您學會 tooretrieve hello 主機名稱、 連接埠和金鑰使用方式 tooconnect tooan Azure Redis 快取執行個體。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 tooretrieve hello 主機名稱、 金鑰和 Azure Redis 快取執行個體的連接埠的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | 取得 Azure Redis Cache 執行個體的詳細資料。 |
| [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) | 取得 Azure Redis Cache 執行個體的存取金鑰。 |


## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他的 Azure Redis 快取 CLI 指令碼範例可以在 hello [Azure Redis 快取文件](../cli-samples.md)。
