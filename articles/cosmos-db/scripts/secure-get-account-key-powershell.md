---
title: "aaaAzure PowerShell 指令碼取得帳戶金鑰 cosmosdb |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 取得 cosmosdb 的帳戶金鑰"
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
ms.openlocfilehash: 9ccee3085dc4fa6507d43e4a220dd5fc32889a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-powershell"></a><span data-ttu-id="30f28-103">使用 PowerShell 取得 Azure Cosmos DB 的帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="30f28-103">Get account keys for Azure Cosmos DB using PowerShell</span></span>

<span data-ttu-id="30f28-104">這個範例會取得任何一種 Azure Cosmos DB 帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="30f28-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="30f28-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="30f28-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "Get hello keys for an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="30f28-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="30f28-106">Clean up deployment</span></span>

<span data-ttu-id="30f28-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="30f28-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="30f28-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="30f28-108">Script explanation</span></span>

<span data-ttu-id="30f28-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="30f28-109">This script uses hello following commands.</span></span> <span data-ttu-id="30f28-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="30f28-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="30f28-111">命令</span><span class="sxs-lookup"><span data-stu-id="30f28-111">Command</span></span> | <span data-ttu-id="30f28-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="30f28-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="30f28-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="30f28-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="30f28-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="30f28-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="30f28-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="30f28-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="30f28-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="30f28-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="30f28-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="30f28-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="30f28-118">叫用在 hello Azure CosmosDB 帳戶的動作。</span><span class="sxs-lookup"><span data-stu-id="30f28-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="30f28-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="30f28-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="30f28-120">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="30f28-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="30f28-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30f28-121">Next steps</span></span>

<span data-ttu-id="30f28-122">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/)。</span><span class="sxs-lookup"><span data-stu-id="30f28-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="30f28-123">其他 Azure Cosmos DB PowerShell 指令碼範例可以在 hello [Azure Cosmos DB PowerShell 指令碼](../powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="30f28-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
