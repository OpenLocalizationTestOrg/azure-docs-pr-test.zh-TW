---
title: "使用 Powershell 指令碼的 Azure 搜尋 aaaManage |Microsoft 文件"
description: "使用 PowerShell 指令碼管理 Azure 搜尋服務。 建立或更新 Azure 搜尋服務，並管理 Azure 搜尋服務的系統管理金鑰"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a>使用 PowerShell 管理 Azure 搜尋服務
> [!div class="op_single_selector"]
> * [入口網站](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

本主題描述 hello PowerShell 命令 tooperform 許多 hello Azure 搜尋服務的管理工作。 我們將逐步建立搜尋服務、調整及管理其 API 金鑰。
這些命令的平行 hello 管理選項提供 hello [Azure 搜尋管理 REST API](http://msdn.microsoft.com/library/dn832684.aspx)。

## <a name="prerequisites"></a>必要條件
* 您必須有 Azure PowerShell 1.0 或更新版本。 如需指示，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。
* 您必須登入 tooyour 如下所述的 PowerShell 中的 Azure 訂用帳戶。

首先，您必須使用此命令的登入 tooAzure:

    Login-AzureRmAccount

Hello Microsoft Azure 登入 對話方塊中指定您的 Azure 帳戶並將其密碼的 hello 電子郵件地址。

或者，您可以 [非互動的方式使用服務主體登入](../azure-resource-manager/resource-group-authenticate-service-principal.md)。

如果您有多個 Azure 訂用帳戶，您需要 tooset 您 Azure 訂用帳戶。 toosee 一份您目前的訂用帳戶，執行此命令。

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello 訂用帳戶，執行下列命令的 hello。 在下列範例的 hello，hello 訂用帳戶名稱是`ContosoSubscription`。

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>命令 toohelp 快速入門
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a>後續步驟
現在，建立您的服務時，您可以採取 hello 接下來的步驟： 建置[索引](search-what-is-an-index.md)，[查詢索引](search-query-overview.md)，最後建立並管理自己的搜尋應用程式使用 Azure 搜尋。

* [在 hello Azure 入口網站中建立 Azure 搜尋索引](search-create-index-portal.md)
* [查詢 Azure 搜尋索引使用 hello Azure 入口網站中的搜尋總管](search-explorer.md)
* [安裝程式從其他服務的索引子 tooload 資料](search-indexer-overview.md)
* [如何在.NET 中的 toouse Azure 搜尋](search-howto-dotnet-sdk.md)
* [分析 Azure 搜尋服務的流量](search-traffic-analytics.md)

