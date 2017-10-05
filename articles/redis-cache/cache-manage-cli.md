---
title: "使用 Azure CLI 管理 Azure Redis Cache | Microsoft Docs"
description: "了解如何在任何平台上安裝 Azure CLI、如何使用它來連接到您的 Azure 帳戶，以及如何從 Azure CLI 建立和管理 Redis 快取。"
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
ms.openlocfilehash: ba078a870a3998568170cc197bd6698b97b7fadb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-azure-redis-cache-using-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="ad747-103">如何使用 Azure 命令列介面 (Azure CLI) 建立並管理 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="ad747-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad747-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad747-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="ad747-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ad747-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="ad747-106">Azure CLI 是從任何平台管理 Azure 基礎結構的一個好方法。</span><span class="sxs-lookup"><span data-stu-id="ad747-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="ad747-107">本文將說明如何使用 Azure CLI 建立並管理 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="ad747-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="ad747-108">此文章適用於舊版 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="ad747-108">This article applies to a previous version of Azure CLI.</span></span> <span data-ttu-id="ad747-109">對於最新的 Azure CLI 2.0 範例指令碼，請參閱 [Azure CLI Redis 快取範例](cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="ad747-109">For the latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ad747-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ad747-110">Prerequisites</span></span>
<span data-ttu-id="ad747-111">若要使用 Azure CLI 建立並管理 Azure Redis 快取執行個體，您必須完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ad747-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span></span>

* <span data-ttu-id="ad747-112">您必須具有 Azure 帳號。</span><span class="sxs-lookup"><span data-stu-id="ad747-112">You must have an Azure account.</span></span> <span data-ttu-id="ad747-113">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/) 。</span><span class="sxs-lookup"><span data-stu-id="ad747-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="ad747-114">[安裝 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="ad747-114">[Install the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="ad747-115">使用個人 Azure 帳戶，或是使用工作或學校的 Azure 帳戶連接 Azure CLI 安裝，並使用 `azure login` 命令從 Azure CLI 登入。</span><span class="sxs-lookup"><span data-stu-id="ad747-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span></span> <span data-ttu-id="ad747-116">若要了解其中的差異和選擇，請參閱 [從 Azure 命令列介面 (Azure CLI) 連線到 Azure 訂用帳戶](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="ad747-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="ad747-117">在執行以下任何命令之前，執行 `azure config mode arm` 命令將 Azure CLI 切換至資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="ad747-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span></span> <span data-ttu-id="ad747-118">如需詳細資訊，請參閱[使用 Azure CLI 管理 Azure 資源和資源群組](../xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="ad747-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="ad747-119">Redis 快取屬性</span><span class="sxs-lookup"><span data-stu-id="ad747-119">Redis Cache properties</span></span>
<span data-ttu-id="ad747-120">當建立並更新 Redis 快取執行個體時會使用下列屬性。</span><span class="sxs-lookup"><span data-stu-id="ad747-120">The following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="ad747-121">屬性</span><span class="sxs-lookup"><span data-stu-id="ad747-121">Property</span></span> | <span data-ttu-id="ad747-122">Switch</span><span class="sxs-lookup"><span data-stu-id="ad747-122">Switch</span></span> | <span data-ttu-id="ad747-123">說明</span><span class="sxs-lookup"><span data-stu-id="ad747-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad747-124">名稱</span><span class="sxs-lookup"><span data-stu-id="ad747-124">name</span></span> |<span data-ttu-id="ad747-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="ad747-125">-n, --name</span></span> |<span data-ttu-id="ad747-126">Redis 快取的名稱。</span><span class="sxs-lookup"><span data-stu-id="ad747-126">Name of the Redis Cache.</span></span> |
| <span data-ttu-id="ad747-127">資源群組</span><span class="sxs-lookup"><span data-stu-id="ad747-127">resource group</span></span> |<span data-ttu-id="ad747-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="ad747-128">-g, --resource-group</span></span> |<span data-ttu-id="ad747-129">資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="ad747-129">Name of the Resource Group.</span></span> |
| <span data-ttu-id="ad747-130">location</span><span class="sxs-lookup"><span data-stu-id="ad747-130">location</span></span> |<span data-ttu-id="ad747-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="ad747-131">-l, --location</span></span> |<span data-ttu-id="ad747-132">要建立快取的位置。</span><span class="sxs-lookup"><span data-stu-id="ad747-132">Location to create cache.</span></span> |
| <span data-ttu-id="ad747-133">size</span><span class="sxs-lookup"><span data-stu-id="ad747-133">size</span></span> |<span data-ttu-id="ad747-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="ad747-134">-z, --size</span></span> |<span data-ttu-id="ad747-135">Redis 快取的大小。</span><span class="sxs-lookup"><span data-stu-id="ad747-135">Size of the Redis Cache.</span></span> <span data-ttu-id="ad747-136">有效的值：[C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="ad747-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="ad747-137">sku</span><span class="sxs-lookup"><span data-stu-id="ad747-137">sku</span></span> |<span data-ttu-id="ad747-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="ad747-138">-x, --sku</span></span> |<span data-ttu-id="ad747-139">Redis SKU。</span><span class="sxs-lookup"><span data-stu-id="ad747-139">Redis SKU.</span></span> <span data-ttu-id="ad747-140">應為其中一個：[Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="ad747-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="ad747-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="ad747-141">EnableNonSslPort</span></span> |<span data-ttu-id="ad747-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="ad747-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="ad747-143">Redis 快取的 EnableNonSslPort 屬性。</span><span class="sxs-lookup"><span data-stu-id="ad747-143">EnableNonSslPort property of the Redis Cache.</span></span> <span data-ttu-id="ad747-144">如果您想針對您的快取啟用非 SSL 連接埠，則加入此旗標</span><span class="sxs-lookup"><span data-stu-id="ad747-144">Add this flag if you want to enable the Non SSL Port for your cache</span></span> |
| <span data-ttu-id="ad747-145">Redis 組態</span><span class="sxs-lookup"><span data-stu-id="ad747-145">Redis Configuration</span></span> |<span data-ttu-id="ad747-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="ad747-146">-c, --redis-configuration</span></span> |<span data-ttu-id="ad747-147">Redis 組態。</span><span class="sxs-lookup"><span data-stu-id="ad747-147">Redis Configuration.</span></span> <span data-ttu-id="ad747-148">在這裡輸入組態金鑰和值的 JSON 格式字串。</span><span class="sxs-lookup"><span data-stu-id="ad747-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="ad747-149">格式："{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="ad747-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="ad747-150">Redis 組態</span><span class="sxs-lookup"><span data-stu-id="ad747-150">Redis Configuration</span></span> |<span data-ttu-id="ad747-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="ad747-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="ad747-152">Redis 組態。</span><span class="sxs-lookup"><span data-stu-id="ad747-152">Redis Configuration.</span></span> <span data-ttu-id="ad747-153">在這裡輸入包含組態金鑰和值的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="ad747-153">Enter the path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="ad747-154">檔案項目的格式：{"":"","":""}</span><span class="sxs-lookup"><span data-stu-id="ad747-154">Format for the file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="ad747-155">分區計數</span><span class="sxs-lookup"><span data-stu-id="ad747-155">Shard Count</span></span> |<span data-ttu-id="ad747-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="ad747-156">-r, --shard-count</span></span> |<span data-ttu-id="ad747-157">建立在具有叢集之進階叢集快取的分區數目。</span><span class="sxs-lookup"><span data-stu-id="ad747-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="ad747-158">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="ad747-158">Virtual Network</span></span> |<span data-ttu-id="ad747-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="ad747-159">-v, --virtual-network</span></span> |<span data-ttu-id="ad747-160">當快取是裝載在 VNET 中時，指定確切的虛擬網路 ARM 資源識別碼以將 Redis 快取部署到其中。</span><span class="sxs-lookup"><span data-stu-id="ad747-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="ad747-161">範例格式：/subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="ad747-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="ad747-162">金鑰類型</span><span class="sxs-lookup"><span data-stu-id="ad747-162">key type</span></span> |<span data-ttu-id="ad747-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="ad747-163">-t, --key-type</span></span> |<span data-ttu-id="ad747-164">要更新的金鑰類型。</span><span class="sxs-lookup"><span data-stu-id="ad747-164">Type of key to renew.</span></span> <span data-ttu-id="ad747-165">有效的值：[Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="ad747-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="ad747-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="ad747-166">StaticIP</span></span> |<span data-ttu-id="ad747-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="ad747-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="ad747-168">當快取是裝載在 VNET 中，為快取在子網路中指定唯一 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ad747-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="ad747-169">如果未提供，則會從子網路中為您選擇一個。</span><span class="sxs-lookup"><span data-stu-id="ad747-169">If not provided, one is chosen for you from the subnet.</span></span> |
| <span data-ttu-id="ad747-170">子網路</span><span class="sxs-lookup"><span data-stu-id="ad747-170">Subnet</span></span> |<span data-ttu-id="ad747-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="ad747-171">t, --subnet <subnet></span></span> |<span data-ttu-id="ad747-172">當快取是裝載在 VNET 中，指定要在其中部署快取的子網路。</span><span class="sxs-lookup"><span data-stu-id="ad747-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> |
| <span data-ttu-id="ad747-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ad747-173">VirtualNetwork</span></span> |<span data-ttu-id="ad747-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="ad747-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="ad747-175">當快取是裝載在 VNET 中時，指定確切的虛擬網路 ARM 資源識別碼以將 Redis 快取部署到其中。</span><span class="sxs-lookup"><span data-stu-id="ad747-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="ad747-176">範例格式：/subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="ad747-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="ad747-177">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ad747-177">Subscription</span></span> |<span data-ttu-id="ad747-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="ad747-178">-s, --subscription</span></span> |<span data-ttu-id="ad747-179">訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="ad747-179">The subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="ad747-180">查看所有的 Redis 快取命令</span><span class="sxs-lookup"><span data-stu-id="ad747-180">See all Redis Cache commands</span></span>
<span data-ttu-id="ad747-181">若要查看所有的 Redis 快取命令和參數，請使用 `azure rediscache -h` 命令。</span><span class="sxs-lookup"><span data-stu-id="ad747-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands to manage your Azure Redis Cache(s)
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
    help:    Renew the authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="ad747-182">建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="ad747-182">Create a Redis Cache</span></span>
<span data-ttu-id="ad747-183">若要建立 Redis 快取，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad747-183">To create a Redis Cache, use the following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="ad747-184">如需有關此命令的詳細資訊，請執行 `azure rediscache create -h` 命令。</span><span class="sxs-lookup"><span data-stu-id="ad747-184">For more information about this command, run the `azure rediscache create -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -l, --location <location>                                Location to create cache.
    help:      -z, --size <size>                                        Size of the Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of the Redis Cache. Add this flag if you want to enable the Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here. Format for the file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards to create on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="ad747-185">刪除現有的 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="ad747-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="ad747-186">若要刪除 Redis 快取，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad747-186">To delete a Redis Cache, use the following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="ad747-187">如需有關此命令的詳細資訊，請執行 `azure rediscache delete -h` 命令。</span><span class="sxs-lookup"><span data-stu-id="ad747-187">For more information about this command, run the `azure rediscache delete -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which the cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="ad747-188">列出您的訂用帳戶或資源群組中所有的 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="ad747-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="ad747-189">若要列出您的訂用帳戶或資源群組中所有的 Redis 快取，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad747-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="ad747-190">如需有關此命令的詳細資訊，請執行 `azure rediscache list -h` 命令。</span><span class="sxs-lookup"><span data-stu-id="ad747-190">For more information about this command, run the `azure rediscache list -h` command.</span></span>

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
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="ad747-191">顯示現有 Redis 快取的屬性</span><span class="sxs-lookup"><span data-stu-id="ad747-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="ad747-192">若要顯示現有的 Redis 快取屬性，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad747-192">To show properties of an existing Redis Cache, use the following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="ad747-193">如需有關此命令的詳細資訊，請執行 `azure rediscache show -h` 命令。</span><span class="sxs-lookup"><span data-stu-id="ad747-193">For more information about this command, run the `azure rediscache show -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="ad747-194">變更現有 Redis 快取的設定</span><span class="sxs-lookup"><span data-stu-id="ad747-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="ad747-195">若要變更現有的 Redis 快取設定，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad747-195">To change settings of an existing Redis Cache, use the following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="ad747-196">如需有關此命令的詳細資訊，請執行 `azure rediscache set -h` 命令。</span><span class="sxs-lookup"><span data-stu-id="ad747-196">For more information about this command, run the `azure rediscache set -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-the-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="ad747-197">更新現有的 Redis 快取驗證金鑰</span><span class="sxs-lookup"><span data-stu-id="ad747-197">Renew the authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="ad747-198">若要更新現有 Redis 快取的驗證金鑰，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad747-198">To renew the authentication key for an existing Redis Cache, use the following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="ad747-199">針對 `key-type` 指定 `Primary` 或 `Secondary`。</span><span class="sxs-lookup"><span data-stu-id="ad747-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="ad747-200">如需有關此命令的詳細資訊，請執行 `azure rediscache renew-key -h` 命令。</span><span class="sxs-lookup"><span data-stu-id="ad747-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew the authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key to renew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="ad747-201">列出現有之 Redis 快取的主要和次要金鑰</span><span class="sxs-lookup"><span data-stu-id="ad747-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="ad747-202">若要列出現有之 Redis 快取的主要和次要金鑰，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad747-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="ad747-203">如需有關此命令的詳細資訊，請執行 `azure rediscache list-keys -h` 命令。</span><span class="sxs-lookup"><span data-stu-id="ad747-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
