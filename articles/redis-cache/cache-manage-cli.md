---
title: "Azure Redis 快取使用 Azure CLI aaaManage |Microsoft 文件"
description: "了解如何 tooinstall hello Azure CLI 任何平台上，如何 toouse 它 tooconnect tooyour Azure 帳戶，以及如何 toocreate 及管理從 hello Azure CLI Redis 快取。"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>如何 toocreate 和管理 Azure Redis 快取使用 hello Azure 命令列介面 (Azure CLI)
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Azure CLI](cache-manage-cli.md)
>
>

hello Azure CLI 是很好的方法 toomanage 您從任何平台的 Azure 基礎結構。 本文章將示範如何 toocreate 和管理您使用 Azure CLI hello 的 Azure Redis 快取執行個體。

> [!NOTE]
> 本文適用於 Azure CLI tooa 舊版本。 Hello 最新 Azure CLI 2.0 」 範例指令碼，請參閱[Azure CLI Redis 快取範例](cli-samples.md)。
> 
> 

## <a name="prerequisites"></a>必要條件
toocreate 和管理 Azure Redis 快取執行個體使用 Azure CLI，您必須完成下列步驟的 hello。

* 您必須具有 Azure 帳號。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/) 。
* [安裝 hello Azure CLI](../cli-install-nodejs.md)。
* 連接 Azure CLI 安裝與個人的 Azure 帳戶，或使用工作或學校的 Azure 帳戶，並從登入 hello Azure CLI 使用 hello`azure login`命令。 toounderstand hello 差異和選擇，請參閱[hello Azure 命令列介面 (Azure CLI) 從連接 tooan Azure 訂用帳戶](../xplat-cli-connect.md)。
* 然後再執行任何 hello 下列命令，切換至 Resource Manager 模式 hello Azure CLI 執行 hello`azure config mode arm`命令。 如需詳細資訊，請參閱[使用 hello Azure CLI toomanage Azure 資源與資源群組](../xplat-cli-azure-resource-manager.md)。

## <a name="redis-cache-properties"></a>Redis 快取屬性
hello 下列屬性可在建立和更新 Redis 快取執行個體。

| 屬性 | Switch | 說明 |
| --- | --- | --- |
| 名稱 |-n, --name |Hello Redis 快取的名稱。 |
| 資源群組 |-g, --resource-group |Hello 資源群組的名稱。 |
| location |-l, --location |位置 toocreate 快取。 |
| size |-z, --size |Hello Redis 快取的大小。 有效的值：[C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| sku |-x, --sku |Redis SKU。 應為其中一個：[Basic, Standard, Premium] |
| EnableNonSslPort |-e, --enable-non-ssl-port |EnableNonSslPort hello Redis 快取屬性。 加入這個旗標，如果您想要您的快取 tooenable hello 非 SSL 連接埠 |
| Redis 組態 |-c, --redis-configuration |Redis 組態。 在這裡輸入組態金鑰和值的 JSON 格式字串。 格式："{"":"","":""}" |
| Redis 組態 |-f, --redis-configuration-file |Redis 組態。 輸入 hello 包含組態的索引鍵和值的檔案路徑。 Hello 檔案項目格式: {"":""，"":""} |
| 分區計數 |-r, --shard-count |分區 toocreate Premium 叢集的快取叢集上的數目。 |
| 虛擬網路 |-v, --virtual-network |當裝載您的 VNET 中的快取指定 hello 精確 ARM 資源識別碼 hello 虛擬網路 toodeploy hello redis 快取中。 範例格式：/subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| 金鑰類型 |-t, --key-type |索引鍵 toorenew 的型別。 有效的值：[Primary, Secondary] |
| StaticIP |-p, --static-ip <static-ip> |當裝載您的快取在 VNET 中，指定唯一的 IP 位址 hello 快取的 hello 子網路中。 如果未提供，其中一個會為您選擇從 hello 子網路。 |
| 子網路 |t, --subnet <subnet> |裝載您的快取在 VNET 中，指定哪些 toodeploy hello 快取以 hello hello 子網路名稱。 |
| VirtualNetwork |-v, --virtual-network <virtual-network> |當裝載您的 VNET 中的快取指定 hello 精確 ARM 資源識別碼 hello 虛擬網路 toodeploy hello redis 快取中。 範例格式：/subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| 訂用帳戶 |-s, --subscription |hello 訂用帳戶識別碼。 |

## <a name="see-all-redis-cache-commands"></a>查看所有的 Redis 快取命令
toosee Redis 快取的所有命令和它們的參數，會使用 hello`azure rediscache -h`命令。

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>建立 Redis Cache
toocreate Redis 快取中，使用下列命令的 hello:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

如需有關此命令的詳細資訊，請執行 hello`azure rediscache create -h`命令。

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>刪除現有的 Redis 快取
toodelete Redis 快取中，使用下列命令的 hello:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

如需有關此命令的詳細資訊，請執行 hello`azure rediscache delete -h`命令。

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>列出您的訂用帳戶或資源群組中所有的 Redis 快取
toolist 所有的 Redis 快取，您的訂用帳戶或資源群組中，使用下列命令 hello:

    azure rediscache list [options]

如需有關此命令的詳細資訊，請執行 hello`azure rediscache list -h`命令。

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>顯示現有 Redis 快取的屬性
現有 Redis 快取，tooshow 屬性，請使用下列命令的 hello:

    azure rediscache show [--name <name> --resource-group <resource-group>]

如需有關此命令的詳細資訊，請執行 hello`azure rediscache show -h`命令。

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>變更現有 Redis 快取的設定
toochange 現有 Redis 快取的設定，下列命令使用 hello:

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

如需有關此命令的詳細資訊，請執行 hello`azure rediscache set -h`命令。

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>更新現有的 Redis 快取 hello 驗證金鑰
toorenew hello 現有 Redis 快取，下列命令使用 hello 的驗證金鑰：

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

針對 `key-type` 指定 `Primary` 或 `Secondary`。

如需有關此命令的詳細資訊，請執行 hello`azure rediscache renew-key -h`命令。

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>列出現有之 Redis 快取的主要和次要金鑰
toolist 主要和次要索引鍵的現有 Redis 快取，請使用下列命令的 hello:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

如需有關此命令的詳細資訊，請執行 hello`azure rediscache list-keys -h`命令。

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
