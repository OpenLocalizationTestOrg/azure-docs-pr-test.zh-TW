---
title: "Azure Cosmos DB 自動化 - 使用 Powershell 管理 | Microsoft Docs"
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
ms.openlocfilehash: 25c543528119410dff0684845a713dcb0d6151d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="da4d3-103">使用 PowerShell 建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="da4d3-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="da4d3-104">下列指南說明使用 Azure Powershell 自動管理 Azure Cosmos DB 資料庫帳戶的命令。</span><span class="sxs-lookup"><span data-stu-id="da4d3-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="da4d3-105">它也包含在[多重區域資料庫帳戶][scaling-globally]中管理帳戶金鑰和容錯移轉優先順序的命令。</span><span class="sxs-lookup"><span data-stu-id="da4d3-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="da4d3-106">更新資料庫帳戶可讓您修改一致性原則和新增/移除區域。</span><span class="sxs-lookup"><span data-stu-id="da4d3-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="da4d3-107">如需跨平台管理 Azure Cosmos DB 資料庫帳戶，您可以使用 [Azure CLI](cli-samples.md)、[資源提供者 REST API][rp-rest-api] 或 [Azure 入口網站](create-documentdb-dotnet.md#create-account)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="da4d3-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="da4d3-108">Getting Started</span></span>

<span data-ttu-id="da4d3-109">按照[如何安裝和設定 Azure PowerShell][powershell-install-configure] 的指示進行安裝，並在 Powershell 中登入 Azure Resource Manager 帳戶。</span><span class="sxs-lookup"><span data-stu-id="da4d3-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="da4d3-110">注意事項</span><span class="sxs-lookup"><span data-stu-id="da4d3-110">Notes</span></span>

* <span data-ttu-id="da4d3-111">如果您想要執行下列命令但不需要使用者確認，請在命令附加 `-Force` 旗標。</span><span class="sxs-lookup"><span data-stu-id="da4d3-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="da4d3-112">下列所有命令都是同步的。</span><span class="sxs-lookup"><span data-stu-id="da4d3-112">All the following commands are synchronous.</span></span>

## <span data-ttu-id="da4d3-113"><a id="create-documentdb-account-powershell"></a> 建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="da4d3-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="da4d3-114">此命令可讓您建立 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="da4d3-114">This command allows you to create an Azure Cosmos DB database account.</span></span> <span data-ttu-id="da4d3-115">將新的資料庫帳戶設定為單一區域或有特定[一致性原則](consistency-levels.md)的[多重區域][scaling-globally]。</span><span class="sxs-lookup"><span data-stu-id="da4d3-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="da4d3-116">`<write-region-location>` 資料庫帳戶之寫入區域的位置名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-116">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="da4d3-117">必須有這個位置，容錯移轉優先順序值才能為 0。</span><span class="sxs-lookup"><span data-stu-id="da4d3-117">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="da4d3-118">每個資料庫帳戶必須有一個寫入區域。</span><span class="sxs-lookup"><span data-stu-id="da4d3-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="da4d3-119">`<read-region-location>` 資料庫帳戶之讀取區域的位置名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-119">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="da4d3-120">必須有這個位置，容錯移轉優先順序值才能大於 0。</span><span class="sxs-lookup"><span data-stu-id="da4d3-120">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="da4d3-121">每個資料庫帳戶可以有多個讀取區域。</span><span class="sxs-lookup"><span data-stu-id="da4d3-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="da4d3-122">`<ip-range-filter>` 會以 CIDR 形式指定一組 IP 位址或 IP 位址範圍，以作為所指定資料庫帳戶的允許用戶端 IP 清單。</span><span class="sxs-lookup"><span data-stu-id="da4d3-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="da4d3-123">IP 位址/範圍必須以逗號分隔，而且不得包含任何空格。</span><span class="sxs-lookup"><span data-stu-id="da4d3-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="da4d3-124">如需詳細資訊，請參閱 [Azure Cosmos DB 防火牆支援](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="da4d3-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="da4d3-125">`<default-consistency-level>` Azure Cosmos DB 帳戶的預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="da4d3-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="da4d3-126">如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="da4d3-127">`<max-interval>` 搭配「限定過期」一致性使用時，這個值代表所容許的過期時間量 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="da4d3-128">此值可接受的範圍是 1 - 100。</span><span class="sxs-lookup"><span data-stu-id="da4d3-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="da4d3-129">`<max-staleness-prefix>` 搭配「限定過期」一致性使用時，這個值代表所容許的過期要求數。</span><span class="sxs-lookup"><span data-stu-id="da4d3-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="da4d3-130">此值可接受的範圍是 1 - 2,147,483,647。</span><span class="sxs-lookup"><span data-stu-id="da4d3-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="da4d3-131">`<resource-group-name>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 [Azure 資源群組][azure-resource-groups]的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-132">`<resource-group-location>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 Azure 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="da4d3-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-133">`<database-account-name>` 要建立之 Azure Cosmos DB 資料庫帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span></span> <span data-ttu-id="da4d3-134">只能使用小寫字母、數字及 '-' 字元，且長度必須為 3 到 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="da4d3-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="da4d3-135">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="da4d3-136">注意事項</span><span class="sxs-lookup"><span data-stu-id="da4d3-136">Notes</span></span>
* <span data-ttu-id="da4d3-137">上述範例會建立一個有兩個區域的資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="da4d3-137">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="da4d3-138">也可以建立一個有一個區域 (指定為寫入區域，容錯移轉優先順序值為 0)，或有兩個以上區域的資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="da4d3-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="da4d3-139">如需詳細資訊，請參閱[多重區域資料庫帳戶][scaling-globally]。</span><span class="sxs-lookup"><span data-stu-id="da4d3-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="da4d3-140">locations 必須是已正式推出 Azure Cosmos DB 的區域。</span><span class="sxs-lookup"><span data-stu-id="da4d3-140">The locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="da4d3-141">[Azure 區域頁面](https://azure.microsoft.com/regions/#services)會提供目前的區域清單。</span><span class="sxs-lookup"><span data-stu-id="da4d3-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="da4d3-142"><a id="update-documentdb-account-powershell"></a> 更新 DocumentDB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="da4d3-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="da4d3-143">此命令可讓您更新 Azure Cosmos DB 資料庫帳戶屬性。</span><span class="sxs-lookup"><span data-stu-id="da4d3-143">This command allows you to update your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="da4d3-144">這包括一致性原則，以及資料庫帳戶存在的位置。</span><span class="sxs-lookup"><span data-stu-id="da4d3-144">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="da4d3-145">此命令可讓您新增及移除區域，但不允許您修改容錯移轉優先順序。</span><span class="sxs-lookup"><span data-stu-id="da4d3-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span></span> <span data-ttu-id="da4d3-146">若要修改容錯移轉優先順序，請參閱[下方](#modify-failover-priority-powershell)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="da4d3-147">`<write-region-location>` 資料庫帳戶之寫入區域的位置名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-147">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="da4d3-148">必須有這個位置，容錯移轉優先順序值才能為 0。</span><span class="sxs-lookup"><span data-stu-id="da4d3-148">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="da4d3-149">每個資料庫帳戶必須有一個寫入區域。</span><span class="sxs-lookup"><span data-stu-id="da4d3-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="da4d3-150">`<read-region-location>` 資料庫帳戶之讀取區域的位置名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-150">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="da4d3-151">必須有這個位置，容錯移轉優先順序值才能大於 0。</span><span class="sxs-lookup"><span data-stu-id="da4d3-151">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="da4d3-152">每個資料庫帳戶可以有多個讀取區域。</span><span class="sxs-lookup"><span data-stu-id="da4d3-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="da4d3-153">`<default-consistency-level>` Azure Cosmos DB 帳戶的預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="da4d3-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="da4d3-154">如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="da4d3-155">`<ip-range-filter>` 會以 CIDR 形式指定一組 IP 位址或 IP 位址範圍，以作為所指定資料庫帳戶的允許用戶端 IP 清單。</span><span class="sxs-lookup"><span data-stu-id="da4d3-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="da4d3-156">IP 位址/範圍必須以逗號分隔，而且不得包含任何空格。</span><span class="sxs-lookup"><span data-stu-id="da4d3-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="da4d3-157">如需詳細資訊，請參閱 [Azure Cosmos DB 防火牆支援](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="da4d3-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="da4d3-158">`<max-interval>` 搭配「限定過期」一致性使用時，這個值代表所容許的過期時間量 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="da4d3-159">此值可接受的範圍是 1 - 100。</span><span class="sxs-lookup"><span data-stu-id="da4d3-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="da4d3-160">`<max-staleness-prefix>` 搭配「限定過期」一致性使用時，這個值代表所容許的過期要求數。</span><span class="sxs-lookup"><span data-stu-id="da4d3-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="da4d3-161">此值可接受的範圍是 1 - 2,147,483,647。</span><span class="sxs-lookup"><span data-stu-id="da4d3-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="da4d3-162">`<resource-group-name>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 [Azure 資源群組][azure-resource-groups]的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-163">`<resource-group-location>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 Azure 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="da4d3-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-164">`<database-account-name>` 要更新之 Azure Cosmos DB 資料庫帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span></span>

<span data-ttu-id="da4d3-165">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="da4d3-166"><a id="delete-documentdb-account-powershell"></a> 刪除 DocumentDB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="da4d3-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="da4d3-167">此命令可讓您刪除現有的 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="da4d3-167">This command allows you to delete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="da4d3-168">`<resource-group-name>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 [Azure 資源群組][azure-resource-groups]的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-169">`<database-account-name>` 要刪除之 Azure Cosmos DB 資料庫帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span></span>

<span data-ttu-id="da4d3-170">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="da4d3-171"><a id="get-documentdb-properties-powershell"></a> 取得 DocumentDB 資料庫帳戶的屬性</span><span class="sxs-lookup"><span data-stu-id="da4d3-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="da4d3-172">此命令可讓您取得現有 Azure Cosmos DB 資料庫帳戶的屬性。</span><span class="sxs-lookup"><span data-stu-id="da4d3-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="da4d3-173">`<resource-group-name>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 [Azure 資源群組][azure-resource-groups]的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-174">`<database-account-name>` Azure Cosmos DB 資料庫帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="da4d3-175">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="da4d3-176"><a id="update-tags-powershell"></a> 更新 Azure Cosmos DB 資料庫帳戶的標記</span><span class="sxs-lookup"><span data-stu-id="da4d3-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="da4d3-177">下列範例說明如何設定 Azure Cosmos DB 資料庫帳戶的 [Azure 資源標記][azure-resource-tags]。</span><span class="sxs-lookup"><span data-stu-id="da4d3-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="da4d3-178">此命令可以透過附加 `-Tags` 旗標與對應的參數，來結合建立或更新命令。</span><span class="sxs-lookup"><span data-stu-id="da4d3-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span></span>

<span data-ttu-id="da4d3-179">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="da4d3-180"><a id="list-account-keys-powershell"></a> 列出帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="da4d3-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="da4d3-181">當您建立 Azure Cosmos DB 帳戶時，服務會產生兩個主要存取金鑰，用於存取 Azure Cosmos DB 帳戶時的驗證。</span><span class="sxs-lookup"><span data-stu-id="da4d3-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="da4d3-182">透過提供這兩個存取金鑰，Azure Cosmos DB 讓您可以重新產生金鑰，同時又不需中斷 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="da4d3-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> <span data-ttu-id="da4d3-183">也提供驗證唯讀作業的唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="da4d3-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="da4d3-184">有兩個讀寫金鑰 (主要和次要) 和兩個唯讀金鑰 (主要和次要)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="da4d3-185">`<resource-group-name>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 [Azure 資源群組][azure-resource-groups]的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-186">`<database-account-name>` Azure Cosmos DB 資料庫帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="da4d3-187">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="da4d3-188"><a id="list-connection-strings-powershell"></a> 列出連接字串</span><span class="sxs-lookup"><span data-stu-id="da4d3-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="da4d3-189">對於 MongoDB 帳戶，您可以使用下列命令來擷取將您的 MongoDB 應用程式連線到資料庫帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="da4d3-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="da4d3-190">`<resource-group-name>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 [Azure 資源群組][azure-resource-groups]的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-191">`<database-account-name>` Azure Cosmos DB 資料庫帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="da4d3-192">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="da4d3-193"><a id="regenerate-account-key-powershell"></a> 重新產生帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="da4d3-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="da4d3-194">您應定期變更 Azure Cosmos DB 帳戶的存取金鑰，讓連線更加安全。</span><span class="sxs-lookup"><span data-stu-id="da4d3-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="da4d3-195">指派的兩個存取金鑰可讓您在重新產生一個存取金鑰的同時，使用另一個存取金鑰維持 Azure Cosmos DB 帳戶連線。</span><span class="sxs-lookup"><span data-stu-id="da4d3-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="da4d3-196">`<resource-group-name>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 [Azure 資源群組][azure-resource-groups]的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-197">`<database-account-name>` Azure Cosmos DB 資料庫帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="da4d3-198">`<key-kind>` 您想要重新產生的其中一種金鑰類型：["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"]。</span><span class="sxs-lookup"><span data-stu-id="da4d3-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="da4d3-199">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="da4d3-200"><a id="modify-failover-priority-powershell"></a> 修改 Azure Cosmos DB 資料庫帳戶的容錯移轉優先順序</span><span class="sxs-lookup"><span data-stu-id="da4d3-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="da4d3-201">如果是多重區域資料庫帳戶，您可以變更 Azure Cosmos DB 資料庫帳戶所在之不同區域的容錯移轉優先順序。</span><span class="sxs-lookup"><span data-stu-id="da4d3-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="da4d3-202">如需有關 Azure Cosmos DB 資料庫帳戶中容錯移轉的詳細資訊，請參閱[使用 Azure Cosmos DB 全域散發資料][distribute-data-globally]。</span><span class="sxs-lookup"><span data-stu-id="da4d3-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="da4d3-203">`<write-region-location>` 資料庫帳戶之寫入區域的位置名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-203">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="da4d3-204">必須有這個位置，容錯移轉優先順序值才能為 0。</span><span class="sxs-lookup"><span data-stu-id="da4d3-204">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="da4d3-205">每個資料庫帳戶必須有一個寫入區域。</span><span class="sxs-lookup"><span data-stu-id="da4d3-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="da4d3-206">`<read-region-location>` 資料庫帳戶之讀取區域的位置名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-206">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="da4d3-207">必須有這個位置，容錯移轉優先順序值才能大於 0。</span><span class="sxs-lookup"><span data-stu-id="da4d3-207">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="da4d3-208">每個資料庫帳戶可以有多個讀取區域。</span><span class="sxs-lookup"><span data-stu-id="da4d3-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="da4d3-209">`<resource-group-name>` 新的 Azure Cosmos DB 資料庫帳戶所屬的 [Azure 資源群組][azure-resource-groups]的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="da4d3-210">`<database-account-name>` Azure Cosmos DB 資料庫帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="da4d3-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="da4d3-211">範例：</span><span class="sxs-lookup"><span data-stu-id="da4d3-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="da4d3-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da4d3-212">Next steps</span></span>

* <span data-ttu-id="da4d3-213">若要使用 .NET 進行連線，請參閱[使用 .NET 進行連線和查詢](create-documentdb-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-213">To connect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="da4d3-214">若要使用 .NET Core 進行連線，請參閱[使用 .NET Core 進行連線和查詢](create-documentdb-dotnet-core.md)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-214">To connect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="da4d3-215">若要使用 Node.js 進行連線，請參閱[使用 Node.js 和 MongoDB 應用程式進行連線和查詢](create-mongodb-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="da4d3-215">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
