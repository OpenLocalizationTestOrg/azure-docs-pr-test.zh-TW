---
title: "aaaAzure CLI 指令碼範例的 Azure Redis 快取的 Get 詳細資料 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 取得 Azure Redis 快取的詳細資料"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3ad1fdf000bbab52e84dbf9f002a5e9fa6d347a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a>取得 Azure Redis 快取的詳細資料

在此案例中，您學會如何 tooretrieve hello 詳細資料的 Azure Redis 快取執行個體，包括其佈建狀態。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 tooretrieve hello 詳細資料的 Azure Redis 快取執行個體的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | 取得 Azure Redis Cache 執行個體的詳細資料。 |


## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他的 Azure Redis 快取 CLI 指令碼範例可以在 hello [Azure Redis 快取文件](../cli-samples.md)。
