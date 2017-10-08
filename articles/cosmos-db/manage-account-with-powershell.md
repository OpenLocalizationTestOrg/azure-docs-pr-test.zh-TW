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
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>使用 PowerShell 建立 Azure Cosmos DB 帳戶

hello 下列指南說明命令 tooautomate 管理 Azure Cosmos DB 資料庫帳戶使用 Azure Powershell。 它也包含命令 toomanage 帳號金鑰及中的容錯移轉優先權[多區域資料庫帳戶][scaling-globally]。 更新資料庫帳戶可讓您 toomodify 一致性原則和新增/移除區域。 用於跨平台管理您的 Azure Cosmos DB 帳戶，您可以使用[Azure CLI](cli-samples.md)，hello[資源提供者 REST API][rp-rest-api]，或使用 hello [Azure入口網站](create-documentdb-dotnet.md#create-account)。

## <a name="getting-started"></a>開始使用

請依照下列中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell] [ powershell-install-configure] tooinstall 和 tooyour Azure 資源管理員中的記錄在 Powershell 中的帳戶。

### <a name="notes"></a>注意事項

* 如果您想要遵循命令而不需要使用者確認 tooexecute hello，附加 hello `-Force` toohello 命令加上旗標。
* 所有的 hello，下列命令會同步。

## <a id="create-documentdb-account-powershell"></a> 建立 Azure Cosmos DB 帳戶

此命令可讓您 toocreate Azure Cosmos DB 資料庫帳戶。 將新的資料庫帳戶設定為單一區域或有特定[一致性原則](consistency-levels.md)的[多重區域][scaling-globally]。

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`hello 位置名稱的 hello 撰寫 hello 資料庫帳戶的區域。 這個位置是必要的 toohave 容錯移轉優先權值為 0。 每個資料庫帳戶必須有一個寫入區域。
* `<read-region-location>`讀取 hello 資料庫帳戶的區域中的 hello hello 位置名稱。 這個位置是必要的 toohave 容錯移轉優先順序值大於 0。 每個資料庫帳戶可以有多個讀取區域。
* `<ip-range-filter>`CIDR 形式 toobe hello 允許清單適用於給定的資料庫帳戶的用戶端 Ip 包含在指定 IP 位址或 IP 位址範圍的 hello 的組。 IP 位址/範圍必須以逗號分隔，而且不得包含任何空格。 如需詳細資訊，請參閱 [Azure Cosmos DB 防火牆支援](firewall-support.md)
* `<default-consistency-level>`hello 的 hello Azure Cosmos DB 帳戶的預設一致性層級。 如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級](consistency-levels.md)。
* `<max-interval>`繫結失效一致性搭配使用時，這個值代表 hello 時間數量 （以秒為單位） 失效所容許之。 此值可接受的範圍是 1 - 100。
* `<max-staleness-prefix>`繫結失效一致性搭配使用時，這個值代表 hello 所容許之過時的要求數目。 此值可接受的範圍是 1 - 2,147,483,647。
* `<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。
* `<resource-group-location>`所屬 hello 的 hello Azure 資源群組 toowhich hello 新 Azure Cosmos DB 資料庫帳戶的位置。
* `<database-account-name>`建立 hello Azure Cosmos DB 資料庫帳戶 toobe hello 名稱。 它只能使用小寫字母、 數字，hello '-' 字元，而且必須介於 3 到 50 個字元之間。

範例： 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>注意事項
* hello 上述範例會建立資料庫帳戶具有兩個區域。 它也是可能 toocreate 資料庫帳戶與一個區域 （其指定為 hello 寫入區域，已容錯移轉優先權值為 0） 或兩個以上的區域。 如需詳細資訊，請參閱[多重區域資料庫帳戶][scaling-globally]。
* hello 位置必須是的地區 Azure Cosmos DB 上市。 hello 目前區域的清單提供 hello [Azure 區域頁面](https://azure.microsoft.com/regions/#services)。

## <a id="update-documentdb-account-powershell"></a> 更新 DocumentDB 資料庫帳戶

此命令可讓您 tooupdate Azure Cosmos DB 資料庫帳戶屬性。 這包括 hello 一致性原則和 hello 位置中存在哪些 hello 資料庫帳戶。

> [!NOTE]
> 此命令可讓您 tooadd 和移除區域，但不允許您 toomodify 容錯移轉優先權。 toomodify 容錯移轉優先權，請參閱[下方](#modify-failover-priority-powershell)。

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`hello 位置名稱的 hello 撰寫 hello 資料庫帳戶的區域。 這個位置是必要的 toohave 容錯移轉優先權值為 0。 每個資料庫帳戶必須有一個寫入區域。
* `<read-region-location>`讀取 hello 資料庫帳戶的區域中的 hello hello 位置名稱。 這個位置是必要的 toohave 容錯移轉優先順序值大於 0。 每個資料庫帳戶可以有多個讀取區域。
* `<default-consistency-level>`hello 的 hello Azure Cosmos DB 帳戶的預設一致性層級。 如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級](consistency-levels.md)。
* `<ip-range-filter>`CIDR 形式 toobe hello 允許清單適用於給定的資料庫帳戶的用戶端 Ip 包含在指定 IP 位址或 IP 位址範圍的 hello 的組。 IP 位址/範圍必須以逗號分隔，而且不得包含任何空格。 如需詳細資訊，請參閱 [Azure Cosmos DB 防火牆支援](firewall-support.md)
* `<max-interval>`繫結失效一致性搭配使用時，這個值代表 hello 時間數量 （以秒為單位） 失效所容許之。 此值可接受的範圍是 1 - 100。
* `<max-staleness-prefix>`繫結失效一致性搭配使用時，這個值代表 hello 所容許之過時的要求數目。 此值可接受的範圍是 1 - 2,147,483,647。
* `<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。
* `<resource-group-location>`所屬 hello 的 hello Azure 資源群組 toowhich hello 新 Azure Cosmos DB 資料庫帳戶的位置。
* `<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶 toobe 更新名稱。

範例： 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a> 刪除 DocumentDB 資料庫帳戶

此命令可讓您 toodelete 現有 Azure Cosmos DB 資料庫帳戶。

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。
* `<database-account-name>`刪除 hello Azure Cosmos DB 資料庫帳戶 toobe hello 名稱。

範例：

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a> 取得 DocumentDB 資料庫帳戶的屬性

此命令可讓您現有的 Azure Cosmos DB 資料庫帳戶 tooget hello 屬性。

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。
* `<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。

範例：

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a> 更新 Azure Cosmos DB 資料庫帳戶的標記

hello 下列範例將說明如何 tooset [Azure 資源標記][ azure-resource-tags]您 Azure Cosmos 資料庫的資料庫帳戶。

> [!NOTE]
> 此命令可以結合 hello 建立或更新命令藉由附加 hello `-Tags` hello 對應參數的旗標。

範例：

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> 列出帳戶金鑰

當您建立 Azure Cosmos DB 帳戶時，hello 服務就會產生兩個存取 hello Azure Cosmos DB 帳戶時可以用於驗證的主要存取金鑰。 藉由提供兩個存取金鑰，Azure Cosmos DB 可讓您使用不中斷 tooyour Azure Cosmos DB 帳戶 tooregenerate hello 索引鍵。 也提供驗證唯讀作業的唯讀金鑰。 有兩個讀寫金鑰 (主要和次要) 和兩個唯讀金鑰 (主要和次要)。

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。
* `<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。

範例：

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> 列出連接字串

MongoDB 帳戶 hello MongoDB 應用程式 toohello 資料庫帳戶可以使用下列命令的 hello 擷取連接字串 tooconnect。

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。
* `<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。

範例：

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> 重新產生帳戶金鑰

您應該變更 hello 存取金鑰 tooyour Azure Cosmos DB 帳戶 toohelp 定期更新您的連接更安全。 兩個存取金鑰指派 tooenable 您 toomaintain 連線 toohello 使用一個存取金鑰，當您重新產生 Azure Cosmos DB 帳戶 hello 其他存取金鑰。

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。
* `<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。
* `<key-kind>`其中一種 hello 四個索引鍵: ["Primary"|"次要"|"PrimaryReadonly"|"SecondaryReadonly"] 您想要 tooregenerate。

範例：

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> 修改 Azure Cosmos DB 資料庫帳戶的容錯移轉優先順序

多區域資料庫的帳戶，您可以變更各個區域的 hello Azure Cosmos DB 資料庫帳戶存在於 hello hello 容錯移轉優先權。 如需有關 Azure Cosmos DB 資料庫帳戶中容錯移轉的詳細資訊，請參閱[使用 Azure Cosmos DB 全域散發資料][distribute-data-globally]。

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`hello 位置名稱的 hello 撰寫 hello 資料庫帳戶的區域。 這個位置是必要的 toohave 容錯移轉優先權值為 0。 每個資料庫帳戶必須有一個寫入區域。
* `<read-region-location>`讀取 hello 資料庫帳戶的區域中的 hello hello 位置名稱。 這個位置是必要的 toohave 容錯移轉優先順序值大於 0。 每個資料庫帳戶可以有多個讀取區域。
* `<resource-group-name>`hello hello 名稱[Azure 資源群組][ azure-resource-groups] toowhich hello 新 Azure Cosmos DB 資料庫的帳戶屬於。
* `<database-account-name>`hello hello Azure Cosmos DB 資料庫帳戶名稱。

範例：

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>後續步驟

* tooconnect 使用.NET，請參閱[連接和查詢的.NET](create-documentdb-dotnet.md)。
* 使用.NET Core tooconnect 看到[連接和查詢使用.NET Core](create-documentdb-dotnet-core.md)。
* tooconnect 使用 Node.js，請參閱[連接和使用 Node.js 和 MongoDB 應用程式查詢](create-mongodb-nodejs.md)。

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
