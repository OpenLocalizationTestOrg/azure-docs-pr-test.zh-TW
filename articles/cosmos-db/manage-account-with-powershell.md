---
title: "aaaAzure Cosmos DB 自動化-使用 Powershell 管理 |Microsoft 文件"
description: "使用 Azure Powershell 管理 Azure Cosmos DB 資料庫帳戶。"
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="37232-103">使用 PowerShell 建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="37232-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="37232-104">hello 下列指南說明命令 tooautomate 管理 Azure Cosmos DB 資料庫帳戶使用 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="37232-104">hello following guide describes commands tooautomate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="37232-105">它也包含命令 toomanage 帳號金鑰及中的容錯移轉優先權[多區域資料庫帳戶][scaling-globally]。</span><span class="sxs-lookup"><span data-stu-id="37232-105">It also includes commands toomanage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="37232-106">更新資料庫帳戶可讓您 toomodify 一致性原則和新增/移除區域。</span><span class="sxs-lookup"><span data-stu-id="37232-106">Updating your database account allows you toomodify consistency policies and add/remove regions.</span></span> <span data-ttu-id="37232-107">用於跨平台管理您的 Azure Cosmos DB 帳戶，您可以使用[Azure CLI](cli-samples.md)，hello[資源提供者 REST API][rp-rest-api]，或使用 hello [Azure入口網站](create-documentdb-dotnet.md#create-account)。</span><span class="sxs-lookup"><span data-stu-id="37232-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), hello [Resource Provider REST API][rp-rest-api], or hello [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="37232-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="37232-108">Getting Started</span></span>

<span data-ttu-id="37232-109">請依照下列中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell] [ powershell-install-configure] tooinstall 和 tooyour Azure 資源管理員中的記錄在 Powershell 中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="37232-109">Follow hello instructions in [How tooinstall and configure Azure PowerShell][powershell-install-configure] tooinstall and log in tooyour Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="37232-110">注意事項</span><span class="sxs-lookup"><span data-stu-id="37232-110">Notes</span></span>

* <span data-ttu-id="37232-111">如果您想要遵循命令而不需要使用者確認 tooexecute hello，附加 hello `-Force` toohello 命令加上旗標。</span><span class="sxs-lookup"><span data-stu-id="37232-111">If you would like tooexecute hello following commands without requiring user confirmation, append hello `-Force` flag toohello command.</span></span>
* <span data-ttu-id="37232-112">所有的 hello，下列命令會同步。</span><span class="sxs-lookup"><span data-stu-id="37232-112">All hello following commands are synchronous.</span></span>

## <span data-ttu-id="37232-113"><a id="create-documentdb-account-powershell"></a> 建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="37232-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="37232-114">此命令可讓您 toocreate Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="37232-114">This command allows you toocreate an Azure Cosmos DB database account.</span></span> <span data-ttu-id="37232-115">將新的資料庫帳戶設定為單一區域或有特定[一致性原則](consistency-levels.md)的[多重區域][scaling-globally]。</span><span class="sxs-lookup"><span data-stu-id="37232-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="37232-116">`<write-region-location>`hello 位置名稱的 hello 撰寫 hello 資料庫帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="37232-116">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="37232-117">這個位置是必要的 toohave 容錯移轉優先權值為 0。</span><span class="sxs-lookup"><span data-stu-id="37232-117">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="37232-118">每個資料庫帳戶必須有一個寫入區域。</span><span class="sxs-lookup"><span data-stu-id="37232-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="37232-119">`<read-region-location>`讀取 hello 資料庫帳戶的區域中的 hello hello 位置名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-119">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="37232-120">這個位置是必要的 toohave 容錯移轉優先順序值大於 0。</span><span class="sxs-lookup"><span data-stu-id="37232-120">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="37232-121">每個資料庫帳戶可以有多個讀取區域。</span><span class="sxs-lookup"><span data-stu-id="37232-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="37232-122">`<ip-range-filter>`CIDR 形式 toobe hello 允許清單適用於給定的資料庫帳戶的用戶端 Ip 包含在指定 IP 位址或 IP 位址範圍的 hello 的組。</span><span class="sxs-lookup"><span data-stu-id="37232-122">`<ip-range-filter>` Specifies hello set of IP addresses or IP address ranges in CIDR form toobe included as hello allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="37232-123">IP 位址/範圍必須以逗號分隔，而且不得包含任何空格。</span><span class="sxs-lookup"><span data-stu-id="37232-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="37232-124">如需詳細資訊，請參閱 [Azure Cosmos DB 防火牆支援](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="37232-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="37232-125">`<default-consistency-level>`hello 的 hello Azure Cosmos DB 帳戶的預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="37232-125">`<default-consistency-level>` hello default consistency level of hello Azure Cosmos DB account.</span></span> <span data-ttu-id="37232-126">如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="37232-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="37232-127">`<max-interval>`繫結失效一致性搭配使用時，這個值代表 hello 時間數量 （以秒為單位） 失效所容許之。</span><span class="sxs-lookup"><span data-stu-id="37232-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents hello time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="37232-128">此值可接受的範圍是 1 - 100。</span><span class="sxs-lookup"><span data-stu-id="37232-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="37232-129">`<max-staleness-prefix>`繫結失效一致性搭配使用時，這個值代表 hello 所容許之過時的要求數目。</span><span class="sxs-lookup"><span data-stu-id="37232-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents hello number of stale requests tolerated.</span></span> <span data-ttu-id="37232-130">此值可接受的範圍是 1 - 2,147,483,647。</span><span class="sxs-lookup"><span data-stu-id="37232-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="37232-131">`<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。</span><span class="sxs-lookup"><span data-stu-id="37232-131">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-132">`<resource-group-location>`所屬 hello 的 hello Azure 資源群組 toowhich hello 新 Azure Cosmos DB 資料庫帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="37232-132">`<resource-group-location>` hello location of hello Azure Resource Group toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-133">`<database-account-name>`建立 hello Azure Cosmos DB 資料庫帳戶 toobe hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-133">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe created.</span></span> <span data-ttu-id="37232-134">它只能使用小寫字母、 數字，hello '-' 字元，而且必須介於 3 到 50 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="37232-134">It can only use lowercase letters, numbers, hello '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="37232-135">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="37232-136">注意事項</span><span class="sxs-lookup"><span data-stu-id="37232-136">Notes</span></span>
* <span data-ttu-id="37232-137">hello 上述範例會建立資料庫帳戶具有兩個區域。</span><span class="sxs-lookup"><span data-stu-id="37232-137">hello preceding example creates a database account with two regions.</span></span> <span data-ttu-id="37232-138">它也是可能 toocreate 資料庫帳戶與一個區域 （其指定為 hello 寫入區域，已容錯移轉優先權值為 0） 或兩個以上的區域。</span><span class="sxs-lookup"><span data-stu-id="37232-138">It is also possible toocreate a database account with either one region (which is designated as hello write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="37232-139">如需詳細資訊，請參閱[多重區域資料庫帳戶][scaling-globally]。</span><span class="sxs-lookup"><span data-stu-id="37232-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="37232-140">hello 位置必須是的地區 Azure Cosmos DB 上市。</span><span class="sxs-lookup"><span data-stu-id="37232-140">hello locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="37232-141">hello 目前區域的清單提供 hello [Azure 區域頁面](https://azure.microsoft.com/regions/#services)。</span><span class="sxs-lookup"><span data-stu-id="37232-141">hello current list of regions is provided on hello [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="37232-142"><a id="update-documentdb-account-powershell"></a> 更新 DocumentDB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="37232-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="37232-143">此命令可讓您 tooupdate Azure Cosmos DB 資料庫帳戶屬性。</span><span class="sxs-lookup"><span data-stu-id="37232-143">This command allows you tooupdate your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="37232-144">這包括 hello 一致性原則和 hello 位置中存在哪些 hello 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="37232-144">This includes hello consistency policy and hello locations which hello database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="37232-145">此命令可讓您 tooadd 和移除區域，但不允許您 toomodify 容錯移轉優先權。</span><span class="sxs-lookup"><span data-stu-id="37232-145">This command allows you tooadd and remove regions but does not allow you toomodify failover priorities.</span></span> <span data-ttu-id="37232-146">toomodify 容錯移轉優先權，請參閱[下方](#modify-failover-priority-powershell)。</span><span class="sxs-lookup"><span data-stu-id="37232-146">toomodify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="37232-147">`<write-region-location>`hello 位置名稱的 hello 撰寫 hello 資料庫帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="37232-147">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="37232-148">這個位置是必要的 toohave 容錯移轉優先權值為 0。</span><span class="sxs-lookup"><span data-stu-id="37232-148">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="37232-149">每個資料庫帳戶必須有一個寫入區域。</span><span class="sxs-lookup"><span data-stu-id="37232-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="37232-150">`<read-region-location>`讀取 hello 資料庫帳戶的區域中的 hello hello 位置名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-150">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="37232-151">這個位置是必要的 toohave 容錯移轉優先順序值大於 0。</span><span class="sxs-lookup"><span data-stu-id="37232-151">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="37232-152">每個資料庫帳戶可以有多個讀取區域。</span><span class="sxs-lookup"><span data-stu-id="37232-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="37232-153">`<default-consistency-level>`hello 的 hello Azure Cosmos DB 帳戶的預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="37232-153">`<default-consistency-level>` hello default consistency level of hello Azure Cosmos DB account.</span></span> <span data-ttu-id="37232-154">如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="37232-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="37232-155">`<ip-range-filter>`CIDR 形式 toobe hello 允許清單適用於給定的資料庫帳戶的用戶端 Ip 包含在指定 IP 位址或 IP 位址範圍的 hello 的組。</span><span class="sxs-lookup"><span data-stu-id="37232-155">`<ip-range-filter>` Specifies hello set of IP addresses or IP address ranges in CIDR form toobe included as hello allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="37232-156">IP 位址/範圍必須以逗號分隔，而且不得包含任何空格。</span><span class="sxs-lookup"><span data-stu-id="37232-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="37232-157">如需詳細資訊，請參閱 [Azure Cosmos DB 防火牆支援](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="37232-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="37232-158">`<max-interval>`繫結失效一致性搭配使用時，這個值代表 hello 時間數量 （以秒為單位） 失效所容許之。</span><span class="sxs-lookup"><span data-stu-id="37232-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents hello time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="37232-159">此值可接受的範圍是 1 - 100。</span><span class="sxs-lookup"><span data-stu-id="37232-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="37232-160">`<max-staleness-prefix>`繫結失效一致性搭配使用時，這個值代表 hello 所容許之過時的要求數目。</span><span class="sxs-lookup"><span data-stu-id="37232-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents hello number of stale requests tolerated.</span></span> <span data-ttu-id="37232-161">此值可接受的範圍是 1 - 2,147,483,647。</span><span class="sxs-lookup"><span data-stu-id="37232-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="37232-162">`<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。</span><span class="sxs-lookup"><span data-stu-id="37232-162">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-163">`<resource-group-location>`所屬 hello 的 hello Azure 資源群組 toowhich hello 新 Azure Cosmos DB 資料庫帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="37232-163">`<resource-group-location>` hello location of hello Azure Resource Group toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-164">`<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶 toobe 更新名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-164">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe updated.</span></span>

<span data-ttu-id="37232-165">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="37232-166"><a id="delete-documentdb-account-powershell"></a> 刪除 DocumentDB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="37232-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="37232-167">此命令可讓您 toodelete 現有 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="37232-167">This command allows you toodelete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="37232-168">`<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。</span><span class="sxs-lookup"><span data-stu-id="37232-168">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-169">`<database-account-name>`刪除 hello Azure Cosmos DB 資料庫帳戶 toobe hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-169">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe deleted.</span></span>

<span data-ttu-id="37232-170">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="37232-171"><a id="get-documentdb-properties-powershell"></a> 取得 DocumentDB 資料庫帳戶的屬性</span><span class="sxs-lookup"><span data-stu-id="37232-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="37232-172">此命令可讓您現有的 Azure Cosmos DB 資料庫帳戶 tooget hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="37232-172">This command allows you tooget hello properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="37232-173">`<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。</span><span class="sxs-lookup"><span data-stu-id="37232-173">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-174">`<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-174">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="37232-175">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="37232-176"><a id="update-tags-powershell"></a> 更新 Azure Cosmos DB 資料庫帳戶的標記</span><span class="sxs-lookup"><span data-stu-id="37232-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="37232-177">hello 下列範例將說明如何 tooset [Azure 資源標記][ azure-resource-tags]您 Azure Cosmos 資料庫的資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="37232-177">hello following example describes how tooset [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="37232-178">此命令可以結合 hello 建立或更新命令藉由附加 hello `-Tags` hello 對應參數的旗標。</span><span class="sxs-lookup"><span data-stu-id="37232-178">This command can be combined with hello create or update commands by appending hello `-Tags` flag with hello corresponding parameter.</span></span>

<span data-ttu-id="37232-179">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="37232-180"><a id="list-account-keys-powershell"></a> 列出帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="37232-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="37232-181">當您建立 Azure Cosmos DB 帳戶時，hello 服務就會產生兩個存取 hello Azure Cosmos DB 帳戶時可以用於驗證的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="37232-181">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="37232-182">藉由提供兩個存取金鑰，Azure Cosmos DB 可讓您使用不中斷 tooyour Azure Cosmos DB 帳戶 tooregenerate hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="37232-182">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> <span data-ttu-id="37232-183">也提供驗證唯讀作業的唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="37232-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="37232-184">有兩個讀寫金鑰 (主要和次要) 和兩個唯讀金鑰 (主要和次要)。</span><span class="sxs-lookup"><span data-stu-id="37232-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="37232-185">`<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。</span><span class="sxs-lookup"><span data-stu-id="37232-185">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-186">`<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-186">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="37232-187">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="37232-188"><a id="list-connection-strings-powershell"></a> 列出連接字串</span><span class="sxs-lookup"><span data-stu-id="37232-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="37232-189">MongoDB 帳戶 hello MongoDB 應用程式 toohello 資料庫帳戶可以使用下列命令的 hello 擷取連接字串 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="37232-189">For MongoDB accounts, hello connection string tooconnect your MongoDB app toohello database account can be retrieved using hello following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="37232-190">`<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。</span><span class="sxs-lookup"><span data-stu-id="37232-190">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-191">`<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-191">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="37232-192">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="37232-193"><a id="regenerate-account-key-powershell"></a> 重新產生帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="37232-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="37232-194">您應該變更 hello 存取金鑰 tooyour Azure Cosmos DB 帳戶 toohelp 定期更新您的連接更安全。</span><span class="sxs-lookup"><span data-stu-id="37232-194">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="37232-195">兩個存取金鑰指派 tooenable 您 toomaintain 連線 toohello 使用一個存取金鑰，當您重新產生 Azure Cosmos DB 帳戶 hello 其他存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="37232-195">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="37232-196">`<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。</span><span class="sxs-lookup"><span data-stu-id="37232-196">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-197">`<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-197">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="37232-198">`<key-kind>`其中一種 hello 四個索引鍵: ["Primary"|"次要"|"PrimaryReadonly"|"SecondaryReadonly"] 您想要 tooregenerate。</span><span class="sxs-lookup"><span data-stu-id="37232-198">`<key-kind>` One of hello four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like tooregenerate.</span></span>

<span data-ttu-id="37232-199">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="37232-200"><a id="modify-failover-priority-powershell"></a> 修改 Azure Cosmos DB 資料庫帳戶的容錯移轉優先順序</span><span class="sxs-lookup"><span data-stu-id="37232-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="37232-201">多區域資料庫的帳戶，您可以變更各個區域的 hello Azure Cosmos DB 資料庫帳戶存在於 hello hello 容錯移轉優先權。</span><span class="sxs-lookup"><span data-stu-id="37232-201">For multi-region database accounts, you can change hello failover priority of hello various regions which hello Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="37232-202">如需有關 Azure Cosmos DB 資料庫帳戶中容錯移轉的詳細資訊，請參閱[使用 Azure Cosmos DB 全域散發資料][distribute-data-globally]。</span><span class="sxs-lookup"><span data-stu-id="37232-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="37232-203">`<write-region-location>`hello 位置名稱的 hello 撰寫 hello 資料庫帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="37232-203">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="37232-204">這個位置是必要的 toohave 容錯移轉優先權值為 0。</span><span class="sxs-lookup"><span data-stu-id="37232-204">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="37232-205">每個資料庫帳戶必須有一個寫入區域。</span><span class="sxs-lookup"><span data-stu-id="37232-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="37232-206">`<read-region-location>`讀取 hello 資料庫帳戶的區域中的 hello hello 位置名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-206">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="37232-207">這個位置是必要的 toohave 容錯移轉優先順序值大於 0。</span><span class="sxs-lookup"><span data-stu-id="37232-207">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="37232-208">每個資料庫帳戶可以有多個讀取區域。</span><span class="sxs-lookup"><span data-stu-id="37232-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="37232-209">`<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。</span><span class="sxs-lookup"><span data-stu-id="37232-209">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="37232-210">`<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="37232-210">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="37232-211">範例：</span><span class="sxs-lookup"><span data-stu-id="37232-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="37232-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37232-212">Next steps</span></span>

* <span data-ttu-id="37232-213">tooconnect 使用.NET，請參閱[連接和查詢的.NET](create-documentdb-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="37232-213">tooconnect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="37232-214">使用.NET Core tooconnect 看到[連接和查詢使用.NET Core](create-documentdb-dotnet-core.md)。</span><span class="sxs-lookup"><span data-stu-id="37232-214">tooconnect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="37232-215">tooconnect 使用 Node.js，請參閱[連接和使用 Node.js 和 MongoDB 應用程式查詢](create-mongodb-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="37232-215">tooconnect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
