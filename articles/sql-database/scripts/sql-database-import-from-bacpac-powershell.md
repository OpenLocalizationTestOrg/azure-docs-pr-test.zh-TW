---
title: "aaaPowerShell 範例-匯入的 bacpac 檔案 Azure SQL database |Microsoft 文件"
description: "插入 SQL database 的 azure PowerShell 範例指令碼 tooimport bacpac 磚"
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="84c98-103">使用 PowerShell tooimport bacpac 檔案到 Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="84c98-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="84c98-104">此 PowerShell 指令碼範例會從 **bacpac** 檔案將資料庫匯入 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="84c98-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="84c98-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="84c98-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="84c98-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="84c98-106">Clean up deployment</span></span>

<span data-ttu-id="84c98-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="84c98-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="84c98-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="84c98-108">Script explanation</span></span>

<span data-ttu-id="84c98-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="84c98-109">This script uses hello following commands.</span></span> <span data-ttu-id="84c98-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="84c98-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="84c98-111">命令</span><span class="sxs-lookup"><span data-stu-id="84c98-111">Command</span></span> | <span data-ttu-id="84c98-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="84c98-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="84c98-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84c98-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="84c98-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="84c98-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="84c98-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="84c98-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="84c98-116">建立主機 hello SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="84c98-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="84c98-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="84c98-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="84c98-118">Hello hello 輸入 IP 位址範圍內的伺服器上建立防火牆規則 tooallow 存取 tooall SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="84c98-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="84c98-119">New-AzureRmSqlDatabaseImport (英文)</span><span class="sxs-lookup"><span data-stu-id="84c98-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="84c98-120">匯入的.bacpac 檔案，並在 hello 伺服器上建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="84c98-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="84c98-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84c98-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="84c98-122">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="84c98-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="84c98-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84c98-123">Next steps</span></span>

<span data-ttu-id="84c98-124">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="84c98-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="84c98-125">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="84c98-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
