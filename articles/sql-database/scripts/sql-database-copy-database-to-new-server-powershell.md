---
title: "aaaPowerShell 範例複製 Azure SQL 資料庫新的伺服器 |Microsoft 文件"
description: "Azure PowerShell 範例指令碼 toocopy SQL database tooa 新伺服器"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="222fe-103">使用 PowerShell toocopy SQL database tooa 新伺服器</span><span class="sxs-lookup"><span data-stu-id="222fe-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="222fe-104">此 PowerShell 指令碼範例會在新伺服器中建立現有資料庫的複本。</span><span class="sxs-lookup"><span data-stu-id="222fe-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="222fe-105">複製資料庫 tooa 新伺服器</span><span class="sxs-lookup"><span data-stu-id="222fe-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="222fe-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="222fe-106">Clean up deployment</span></span>

<span data-ttu-id="222fe-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="222fe-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="222fe-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="222fe-108">Script explanation</span></span>

<span data-ttu-id="222fe-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="222fe-109">This script uses hello following commands.</span></span> <span data-ttu-id="222fe-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="222fe-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="222fe-111">命令</span><span class="sxs-lookup"><span data-stu-id="222fe-111">Command</span></span> | <span data-ttu-id="222fe-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="222fe-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="222fe-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="222fe-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="222fe-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="222fe-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="222fe-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="222fe-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="222fe-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="222fe-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="222fe-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="222fe-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="222fe-118">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="222fe-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="222fe-119">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="222fe-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="222fe-120">建立一份使用 hello 快照集在 hello 目前時間的資料庫。</span><span class="sxs-lookup"><span data-stu-id="222fe-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="222fe-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="222fe-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="222fe-122">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="222fe-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="222fe-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="222fe-123">Next steps</span></span>

<span data-ttu-id="222fe-124">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="222fe-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="222fe-125">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="222fe-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
