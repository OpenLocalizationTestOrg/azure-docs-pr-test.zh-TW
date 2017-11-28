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
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="be47b-103">如何 toocreate 和管理 Azure Redis 快取使用 hello Azure 命令列介面 (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="be47b-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be47b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be47b-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="be47b-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="be47b-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="be47b-106">hello Azure CLI 是很好的方法 toomanage 您從任何平台的 Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="be47b-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="be47b-107">本文章將示範如何 toocreate 和管理您使用 Azure CLI hello 的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="be47b-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="be47b-108">本文適用於 Azure CLI tooa 舊版本。</span><span class="sxs-lookup"><span data-stu-id="be47b-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="be47b-109">Hello 最新 Azure CLI 2.0 」 範例指令碼，請參閱[Azure CLI Redis 快取範例](cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="be47b-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="be47b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="be47b-110">Prerequisites</span></span>
<span data-ttu-id="be47b-111">toocreate 和管理 Azure Redis 快取執行個體使用 Azure CLI，您必須完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="be47b-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="be47b-112">您必須具有 Azure 帳號。</span><span class="sxs-lookup"><span data-stu-id="be47b-112">You must have an Azure account.</span></span> <span data-ttu-id="be47b-113">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/) 。</span><span class="sxs-lookup"><span data-stu-id="be47b-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="be47b-114">[安裝 hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="be47b-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="be47b-115">連接 Azure CLI 安裝與個人的 Azure 帳戶，或使用工作或學校的 Azure 帳戶，並從登入 hello Azure CLI 使用 hello`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="be47b-116">toounderstand hello 差異和選擇，請參閱[hello Azure 命令列介面 (Azure CLI) 從連接 tooan Azure 訂用帳戶](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="be47b-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="be47b-117">然後再執行任何 hello 下列命令，切換至 Resource Manager 模式 hello Azure CLI 執行 hello`azure config mode arm`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="be47b-118">如需詳細資訊，請參閱[使用 hello Azure CLI toomanage Azure 資源與資源群組](../xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="be47b-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="be47b-119">Redis 快取屬性</span><span class="sxs-lookup"><span data-stu-id="be47b-119">Redis Cache properties</span></span>
<span data-ttu-id="be47b-120">hello 下列屬性可在建立和更新 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="be47b-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="be47b-121">屬性</span><span class="sxs-lookup"><span data-stu-id="be47b-121">Property</span></span> | <span data-ttu-id="be47b-122">Switch</span><span class="sxs-lookup"><span data-stu-id="be47b-122">Switch</span></span> | <span data-ttu-id="be47b-123">說明</span><span class="sxs-lookup"><span data-stu-id="be47b-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be47b-124">名稱</span><span class="sxs-lookup"><span data-stu-id="be47b-124">name</span></span> |<span data-ttu-id="be47b-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="be47b-125">-n, --name</span></span> |<span data-ttu-id="be47b-126">Hello Redis 快取的名稱。</span><span class="sxs-lookup"><span data-stu-id="be47b-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="be47b-127">資源群組</span><span class="sxs-lookup"><span data-stu-id="be47b-127">resource group</span></span> |<span data-ttu-id="be47b-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="be47b-128">-g, --resource-group</span></span> |<span data-ttu-id="be47b-129">Hello 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="be47b-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="be47b-130">location</span><span class="sxs-lookup"><span data-stu-id="be47b-130">location</span></span> |<span data-ttu-id="be47b-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="be47b-131">-l, --location</span></span> |<span data-ttu-id="be47b-132">位置 toocreate 快取。</span><span class="sxs-lookup"><span data-stu-id="be47b-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="be47b-133">size</span><span class="sxs-lookup"><span data-stu-id="be47b-133">size</span></span> |<span data-ttu-id="be47b-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="be47b-134">-z, --size</span></span> |<span data-ttu-id="be47b-135">Hello Redis 快取的大小。</span><span class="sxs-lookup"><span data-stu-id="be47b-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="be47b-136">有效的值：[C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="be47b-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="be47b-137">sku</span><span class="sxs-lookup"><span data-stu-id="be47b-137">sku</span></span> |<span data-ttu-id="be47b-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="be47b-138">-x, --sku</span></span> |<span data-ttu-id="be47b-139">Redis SKU。</span><span class="sxs-lookup"><span data-stu-id="be47b-139">Redis SKU.</span></span> <span data-ttu-id="be47b-140">應為其中一個：[Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="be47b-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="be47b-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="be47b-141">EnableNonSslPort</span></span> |<span data-ttu-id="be47b-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="be47b-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="be47b-143">EnableNonSslPort hello Redis 快取屬性。</span><span class="sxs-lookup"><span data-stu-id="be47b-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="be47b-144">加入這個旗標，如果您想要您的快取 tooenable hello 非 SSL 連接埠</span><span class="sxs-lookup"><span data-stu-id="be47b-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="be47b-145">Redis 組態</span><span class="sxs-lookup"><span data-stu-id="be47b-145">Redis Configuration</span></span> |<span data-ttu-id="be47b-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="be47b-146">-c, --redis-configuration</span></span> |<span data-ttu-id="be47b-147">Redis 組態。</span><span class="sxs-lookup"><span data-stu-id="be47b-147">Redis Configuration.</span></span> <span data-ttu-id="be47b-148">在這裡輸入組態金鑰和值的 JSON 格式字串。</span><span class="sxs-lookup"><span data-stu-id="be47b-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="be47b-149">格式："{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="be47b-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="be47b-150">Redis 組態</span><span class="sxs-lookup"><span data-stu-id="be47b-150">Redis Configuration</span></span> |<span data-ttu-id="be47b-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="be47b-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="be47b-152">Redis 組態。</span><span class="sxs-lookup"><span data-stu-id="be47b-152">Redis Configuration.</span></span> <span data-ttu-id="be47b-153">輸入 hello 包含組態的索引鍵和值的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="be47b-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="be47b-154">Hello 檔案項目格式: {"":""，"":""}</span><span class="sxs-lookup"><span data-stu-id="be47b-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="be47b-155">分區計數</span><span class="sxs-lookup"><span data-stu-id="be47b-155">Shard Count</span></span> |<span data-ttu-id="be47b-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="be47b-156">-r, --shard-count</span></span> |<span data-ttu-id="be47b-157">分區 toocreate Premium 叢集的快取叢集上的數目。</span><span class="sxs-lookup"><span data-stu-id="be47b-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="be47b-158">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="be47b-158">Virtual Network</span></span> |<span data-ttu-id="be47b-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="be47b-159">-v, --virtual-network</span></span> |<span data-ttu-id="be47b-160">當裝載您的 VNET 中的快取指定 hello 精確 ARM 資源識別碼 hello 虛擬網路 toodeploy hello redis 快取中。</span><span class="sxs-lookup"><span data-stu-id="be47b-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="be47b-161">範例格式：/subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="be47b-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="be47b-162">金鑰類型</span><span class="sxs-lookup"><span data-stu-id="be47b-162">key type</span></span> |<span data-ttu-id="be47b-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="be47b-163">-t, --key-type</span></span> |<span data-ttu-id="be47b-164">索引鍵 toorenew 的型別。</span><span class="sxs-lookup"><span data-stu-id="be47b-164">Type of key toorenew.</span></span> <span data-ttu-id="be47b-165">有效的值：[Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="be47b-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="be47b-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="be47b-166">StaticIP</span></span> |<span data-ttu-id="be47b-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="be47b-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="be47b-168">當裝載您的快取在 VNET 中，指定唯一的 IP 位址 hello 快取的 hello 子網路中。</span><span class="sxs-lookup"><span data-stu-id="be47b-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="be47b-169">如果未提供，其中一個會為您選擇從 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="be47b-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="be47b-170">子網路</span><span class="sxs-lookup"><span data-stu-id="be47b-170">Subnet</span></span> |<span data-ttu-id="be47b-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="be47b-171">t, --subnet <subnet></span></span> |<span data-ttu-id="be47b-172">裝載您的快取在 VNET 中，指定哪些 toodeploy hello 快取以 hello hello 子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="be47b-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="be47b-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="be47b-173">VirtualNetwork</span></span> |<span data-ttu-id="be47b-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="be47b-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="be47b-175">當裝載您的 VNET 中的快取指定 hello 精確 ARM 資源識別碼 hello 虛擬網路 toodeploy hello redis 快取中。</span><span class="sxs-lookup"><span data-stu-id="be47b-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="be47b-176">範例格式：/subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="be47b-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="be47b-177">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="be47b-177">Subscription</span></span> |<span data-ttu-id="be47b-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="be47b-178">-s, --subscription</span></span> |<span data-ttu-id="be47b-179">hello 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="be47b-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="be47b-180">查看所有的 Redis 快取命令</span><span class="sxs-lookup"><span data-stu-id="be47b-180">See all Redis Cache commands</span></span>
<span data-ttu-id="be47b-181">toosee Redis 快取的所有命令和它們的參數，會使用 hello`azure rediscache -h`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

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

## <a name="create-a-redis-cache"></a><span data-ttu-id="be47b-182">建立 Redis Cache</span><span class="sxs-lookup"><span data-stu-id="be47b-182">Create a Redis Cache</span></span>
<span data-ttu-id="be47b-183">toocreate Redis 快取中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be47b-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="be47b-184">如需有關此命令的詳細資訊，請執行 hello`azure rediscache create -h`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

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

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="be47b-185">刪除現有的 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="be47b-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="be47b-186">toodelete Redis 快取中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be47b-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="be47b-187">如需有關此命令的詳細資訊，請執行 hello`azure rediscache delete -h`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

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

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="be47b-188">列出您的訂用帳戶或資源群組中所有的 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="be47b-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="be47b-189">toolist 所有的 Redis 快取，您的訂用帳戶或資源群組中，使用下列命令 hello:</span><span class="sxs-lookup"><span data-stu-id="be47b-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="be47b-190">如需有關此命令的詳細資訊，請執行 hello`azure rediscache list -h`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

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

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="be47b-191">顯示現有 Redis 快取的屬性</span><span class="sxs-lookup"><span data-stu-id="be47b-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="be47b-192">現有 Redis 快取，tooshow 屬性，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be47b-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="be47b-193">如需有關此命令的詳細資訊，請執行 hello`azure rediscache show -h`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

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

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="be47b-194">變更現有 Redis 快取的設定</span><span class="sxs-lookup"><span data-stu-id="be47b-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="be47b-195">toochange 現有 Redis 快取的設定，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="be47b-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="be47b-196">如需有關此命令的詳細資訊，請執行 hello`azure rediscache set -h`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

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

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="be47b-197">更新現有的 Redis 快取 hello 驗證金鑰</span><span class="sxs-lookup"><span data-stu-id="be47b-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="be47b-198">toorenew hello 現有 Redis 快取，下列命令使用 hello 的驗證金鑰：</span><span class="sxs-lookup"><span data-stu-id="be47b-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="be47b-199">針對 `key-type` 指定 `Primary` 或 `Secondary`。</span><span class="sxs-lookup"><span data-stu-id="be47b-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="be47b-200">如需有關此命令的詳細資訊，請執行 hello`azure rediscache renew-key -h`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

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

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="be47b-201">列出現有之 Redis 快取的主要和次要金鑰</span><span class="sxs-lookup"><span data-stu-id="be47b-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="be47b-202">toolist 主要和次要索引鍵的現有 Redis 快取，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be47b-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="be47b-203">如需有關此命令的詳細資訊，請執行 hello`azure rediscache list-keys -h`命令。</span><span class="sxs-lookup"><span data-stu-id="be47b-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

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
