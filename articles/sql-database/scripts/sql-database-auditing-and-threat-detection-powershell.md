---
title: "aaaPowerShell 範例稽核威脅偵測 Azure SQL 資料庫 |Microsoft 文件"
description: "Azure PowerShell 範例指令碼 tooconfigure 稽核與威脅偵測在 Azure SQL 資料庫"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="c51cd-103">使用 PowerShell tooconfigure SQL Database 稽核和威脅偵測</span><span class="sxs-lookup"><span data-stu-id="c51cd-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="c51cd-104">此 PowerShell 指令碼範例會設定 SQL Database 稽核與威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="c51cd-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c51cd-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c51cd-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c51cd-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="c51cd-106">Clean up deployment</span></span>

<span data-ttu-id="c51cd-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="c51cd-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c51cd-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c51cd-108">Script explanation</span></span>

<span data-ttu-id="c51cd-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="c51cd-109">This script uses hello following commands.</span></span> <span data-ttu-id="c51cd-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="c51cd-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c51cd-111">命令</span><span class="sxs-lookup"><span data-stu-id="c51cd-111">Command</span></span> | <span data-ttu-id="c51cd-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="c51cd-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c51cd-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c51cd-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c51cd-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c51cd-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c51cd-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="c51cd-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="c51cd-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="c51cd-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c51cd-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c51cd-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="c51cd-118">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c51cd-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="c51cd-119">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="c51cd-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="c51cd-120">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c51cd-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="c51cd-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="c51cd-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="c51cd-122">設定資料庫的 hello 稽核原則。</span><span class="sxs-lookup"><span data-stu-id="c51cd-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="c51cd-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="c51cd-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="c51cd-124">設定資料庫的威脅偵測原則。</span><span class="sxs-lookup"><span data-stu-id="c51cd-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="c51cd-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c51cd-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c51cd-126">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="c51cd-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c51cd-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c51cd-127">Next steps</span></span>

<span data-ttu-id="c51cd-128">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c51cd-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c51cd-129">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="c51cd-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
