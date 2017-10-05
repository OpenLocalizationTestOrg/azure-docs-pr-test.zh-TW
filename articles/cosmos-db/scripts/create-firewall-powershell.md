---
title: "Azure PowerShell 指令碼：建立 Azure Cosmos DB 的防火牆 | Microsoft Docs"
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
ms.openlocfilehash: caad9212649dd3dc47ddb21555b5b8496c3d2da1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="b75e4-103">Azure Cosmos DB：使用 PowerShell 建立防火牆</span><span class="sxs-lookup"><span data-stu-id="b75e4-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="b75e4-104">這個範例 PowerShell 指令碼會建立適用於任何種類 Azure Cosmos DB API 帳戶的防火牆。</span><span class="sxs-lookup"><span data-stu-id="b75e4-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b75e4-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b75e4-105">Sample script</span></span>

<span data-ttu-id="b75e4-106">[!code-powershell[主要](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "建立 Azure Cosmos DB 的防火牆")]</span><span class="sxs-lookup"><span data-stu-id="b75e4-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b75e4-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="b75e4-107">Clean up deployment</span></span>

<span data-ttu-id="b75e4-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="b75e4-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b75e4-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b75e4-109">Script explanation</span></span>

<span data-ttu-id="b75e4-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="b75e4-110">This script uses the following commands.</span></span> <span data-ttu-id="b75e4-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="b75e4-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b75e4-112">命令</span><span class="sxs-lookup"><span data-stu-id="b75e4-112">Command</span></span> | <span data-ttu-id="b75e4-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="b75e4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b75e4-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b75e4-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="b75e4-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b75e4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b75e4-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b75e4-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="b75e4-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="b75e4-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b75e4-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="b75e4-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="b75e4-119">修改資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="b75e4-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="b75e4-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b75e4-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="b75e4-121">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="b75e4-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b75e4-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b75e4-122">Next steps</span></span>

<span data-ttu-id="b75e4-123">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](https://docs.microsoft.com/powershell/)。</span><span class="sxs-lookup"><span data-stu-id="b75e4-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="b75e4-124">您可以在 [Azure Cosmos DB PowerShell 指令碼](../powershell-samples.md)中找到其他 Azure Cosmos DB PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="b75e4-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>