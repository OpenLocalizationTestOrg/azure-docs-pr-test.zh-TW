---
title: "PowerShell 指令碼建立的 Azure Cosmos DB 防火牆 aaaAzure |Microsoft 文件"
description: "Azure PowerShell 指令碼範例：建立 Azure Cosmos DB 的防火牆"
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
ms.openlocfilehash: 00dd2dd847c7ed0e35f5555c2b87b90977f137f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="0ff6d-103">Azure Cosmos DB：使用 PowerShell 建立防火牆</span><span class="sxs-lookup"><span data-stu-id="0ff6d-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="0ff6d-104">這個範例 PowerShell 指令碼會建立適用於任何種類 Azure Cosmos DB API 帳戶的防火牆。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="0ff6d-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0ff6d-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0ff6d-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="0ff6d-106">Clean up deployment</span></span>

<span data-ttu-id="0ff6d-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0ff6d-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0ff6d-108">Script explanation</span></span>

<span data-ttu-id="0ff6d-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-109">This script uses hello following commands.</span></span> <span data-ttu-id="0ff6d-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0ff6d-111">命令</span><span class="sxs-lookup"><span data-stu-id="0ff6d-111">Command</span></span> | <span data-ttu-id="0ff6d-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="0ff6d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0ff6d-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ff6d-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="0ff6d-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0ff6d-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="0ff6d-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="0ff6d-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="0ff6d-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="0ff6d-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="0ff6d-118">修改 hello 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="0ff6d-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ff6d-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="0ff6d-120">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="0ff6d-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ff6d-121">Next steps</span></span>

<span data-ttu-id="0ff6d-122">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/)。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="0ff6d-123">其他 Azure Cosmos DB PowerShell 指令碼範例可以在 hello [Azure Cosmos DB PowerShell 指令碼](../powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="0ff6d-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
