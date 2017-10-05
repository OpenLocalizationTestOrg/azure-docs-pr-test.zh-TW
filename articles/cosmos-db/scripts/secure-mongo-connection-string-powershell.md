---
title: "Azure PowerShell 指令碼 - 取得 MongoDB 應用程式的 Azure Cosmos DB 連接字串 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 取得 MongoDB 應用程式的 Azure Cosmos DB 連接字串"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: e44e35cc7d11db48cd82e470ce8226b3c8cc220a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="3a358-103">使用 PowerShell 取得 MongoDB 應用程式的 Azure Cosmos DB 連接字串</span><span class="sxs-lookup"><span data-stu-id="3a358-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="3a358-104">此範例會使用 PowerShell 取得 MongoDB 應用程式的 Azure Cosmos DB 連接字串。</span><span class="sxs-lookup"><span data-stu-id="3a358-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="3a358-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="3a358-105">Sample script</span></span>

<span data-ttu-id="3a358-106">[!code-powershell[主要](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "從 Azure Cosmos DB 帳戶取得 MongoDB 連接字串")]</span><span class="sxs-lookup"><span data-stu-id="3a358-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get the MongoDB connection string from an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3a358-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="3a358-107">Clean up deployment</span></span>

<span data-ttu-id="3a358-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="3a358-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="3a358-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="3a358-109">Script explanation</span></span>

<span data-ttu-id="3a358-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="3a358-110">This script uses the following commands.</span></span> <span data-ttu-id="3a358-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="3a358-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3a358-112">命令</span><span class="sxs-lookup"><span data-stu-id="3a358-112">Command</span></span> | <span data-ttu-id="3a358-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="3a358-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a358-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3a358-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="3a358-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3a358-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3a358-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3a358-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="3a358-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="3a358-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="3a358-118">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="3a358-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="3a358-119">在 Azure CosmosDB 帳戶上叫用動作。</span><span class="sxs-lookup"><span data-stu-id="3a358-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="3a358-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3a358-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="3a358-121">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="3a358-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3a358-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a358-122">Next steps</span></span>

<span data-ttu-id="3a358-123">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](https://docs.microsoft.com/powershell/)。</span><span class="sxs-lookup"><span data-stu-id="3a358-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="3a358-124">您可以在 [Azure Cosmos DB PowerShell 指令碼](../powershell-samples.md)中找到其他 Azure Cosmos DB PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="3a358-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>