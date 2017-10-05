---
title: "PowerShell 範例 - 匯入 - bacpac 檔案 - Azure SQL Database | Microsoft Docs"
description: "將 bacpac 圖格匯入 SQL Database 的 Azure PowerShell 範例指令碼"
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
ms.openlocfilehash: 20e1d4c195314d6e828e1dac6afae8be11805b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-import-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="88ad3-103">使用 PowerShell 將 bacpac 檔案匯入 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="88ad3-103">Use PowerShell to import a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="88ad3-104">此 PowerShell 指令碼範例會從 **bacpac** 檔案將資料庫匯入 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="88ad3-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="88ad3-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="88ad3-105">Sample script</span></span>

<span data-ttu-id="88ad3-106">[!code-powershell[主要](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "建立 SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="88ad3-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="88ad3-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="88ad3-107">Clean up deployment</span></span>

<span data-ttu-id="88ad3-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="88ad3-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="88ad3-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="88ad3-109">Script explanation</span></span>

<span data-ttu-id="88ad3-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="88ad3-110">This script uses the following commands.</span></span> <span data-ttu-id="88ad3-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="88ad3-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="88ad3-112">命令</span><span class="sxs-lookup"><span data-stu-id="88ad3-112">Command</span></span> | <span data-ttu-id="88ad3-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="88ad3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="88ad3-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="88ad3-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="88ad3-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="88ad3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="88ad3-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="88ad3-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="88ad3-117">建立主控 SQL Database 的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="88ad3-117">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="88ad3-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="88ad3-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="88ad3-119">建立防火牆規則以允許從輸入的 IP 位址範圍存取伺服器上的所有 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="88ad3-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="88ad3-120">New-AzureRmSqlDatabaseImport (英文)</span><span class="sxs-lookup"><span data-stu-id="88ad3-120">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="88ad3-121">在伺服器上匯入 .bacpac 檔案並建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="88ad3-121">Imports a .bacpac file and create a new database on the server.</span></span> |
| [<span data-ttu-id="88ad3-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="88ad3-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="88ad3-123">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="88ad3-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="88ad3-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88ad3-124">Next steps</span></span>

<span data-ttu-id="88ad3-125">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="88ad3-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="88ad3-126">其他的 SQL Database PowerShell 指令碼範例可於 [Azure SQL Database PowerShell 指令碼](../sql-database-powershell-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="88ad3-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
