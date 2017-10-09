---
title: "aaaPowerShell 範例建立 Azure SQL database |Microsoft 文件"
description: "Azure PowerShell 範例指令碼 toocreate Azure SQL database"
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
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="2c983-103">使用 PowerShell toocreate 單一 Azure SQL 資料庫並設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="2c983-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="2c983-104">此 PowerShell 指令碼範例會建立 Azure SQL Database 並設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="2c983-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="2c983-105">一旦 hello 指令碼順利執行之後，您可以從所有 Azure 服務存取 SQL Database 的 hello 與 hello 設定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2c983-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="2c983-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="2c983-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2c983-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="2c983-107">Clean up deployment</span></span>

<span data-ttu-id="2c983-108">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="2c983-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2c983-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="2c983-109">Script explanation</span></span>

<span data-ttu-id="2c983-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="2c983-110">This script uses hello following commands.</span></span> <span data-ttu-id="2c983-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="2c983-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2c983-112">命令</span><span class="sxs-lookup"><span data-stu-id="2c983-112">Command</span></span> | <span data-ttu-id="2c983-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="2c983-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2c983-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2c983-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2c983-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2c983-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2c983-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="2c983-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="2c983-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="2c983-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="2c983-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="2c983-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="2c983-119">Hello hello 輸入 IP 位址範圍內的伺服器上建立防火牆規則 tooallow 存取 tooall SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2c983-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="2c983-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2c983-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="2c983-121">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="2c983-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="2c983-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2c983-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2c983-123">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="2c983-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2c983-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c983-124">Next steps</span></span>

<span data-ttu-id="2c983-125">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="2c983-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2c983-126">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="2c983-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



