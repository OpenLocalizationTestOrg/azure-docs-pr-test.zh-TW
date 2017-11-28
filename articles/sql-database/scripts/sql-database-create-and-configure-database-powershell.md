---
title: "PowerShell 範例 - 建立 Azure SQL Database | Microsoft Docs"
description: "建立 Azure SQL Database 的 Azure PowerShell 範例指令碼"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1b6809007e6717b7f8847452b2fa5b38d4ab5ccc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="c7f6a-103">使用 PowerShell 建立單一 Azure SQL Database 並設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="c7f6a-103">Use PowerShell to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="c7f6a-104">此 PowerShell 指令碼範例會建立 Azure SQL Database 並設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="c7f6a-105">成功執行指令碼後，即可從所有 Azure 服務和所設定的 IP 位址存取 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c7f6a-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c7f6a-106">Sample script</span></span>

<span data-ttu-id="c7f6a-107">[!code-powershell[主要](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "建立 SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="c7f6a-107">[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c7f6a-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="c7f6a-108">Clean up deployment</span></span>

<span data-ttu-id="c7f6a-109">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-109">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c7f6a-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c7f6a-110">Script explanation</span></span>

<span data-ttu-id="c7f6a-111">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-111">This script uses the following commands.</span></span> <span data-ttu-id="c7f6a-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c7f6a-113">命令</span><span class="sxs-lookup"><span data-stu-id="c7f6a-113">Command</span></span> | <span data-ttu-id="c7f6a-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="c7f6a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c7f6a-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7f6a-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c7f6a-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c7f6a-117">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="c7f6a-117">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="c7f6a-118">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-118">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c7f6a-119">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="c7f6a-119">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="c7f6a-120">建立防火牆規則以允許從輸入的 IP 位址範圍存取伺服器上的所有 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-120">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="c7f6a-121">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c7f6a-121">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="c7f6a-122">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-122">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="c7f6a-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7f6a-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c7f6a-124">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c7f6a-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7f6a-125">Next steps</span></span>

<span data-ttu-id="c7f6a-126">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c7f6a-127">其他的 SQL Database PowerShell 指令碼範例可於 [Azure SQL Database PowerShell 指令碼](../sql-database-powershell-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="c7f6a-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



