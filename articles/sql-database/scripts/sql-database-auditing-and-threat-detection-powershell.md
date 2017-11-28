---
title: "PowerShell 範例 - 稽核 - 威脅偵測 - Azure SQL Database |Microsoft 文件"
description: "在 Azure SQL Database 中設定稽核與威脅偵測的 Azure PowerShell 指令碼範例"
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
ms.openlocfilehash: e039d35474bff3b066a6605a97e04d4a81c365eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="b1105-103">使用 PowerShell 設定 SQL Database 稽核與威脅偵測</span><span class="sxs-lookup"><span data-stu-id="b1105-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="b1105-104">此 PowerShell 指令碼範例會設定 SQL Database 稽核與威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="b1105-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b1105-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b1105-105">Sample script</span></span>

<span data-ttu-id="b1105-106">[!code-powershell[主要](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "設定稽核與威脅偵測")]</span><span class="sxs-lookup"><span data-stu-id="b1105-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b1105-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="b1105-107">Clean up deployment</span></span>

<span data-ttu-id="b1105-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="b1105-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b1105-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b1105-109">Script explanation</span></span>

<span data-ttu-id="b1105-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="b1105-110">This script uses the following commands.</span></span> <span data-ttu-id="b1105-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="b1105-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b1105-112">命令</span><span class="sxs-lookup"><span data-stu-id="b1105-112">Command</span></span> | <span data-ttu-id="b1105-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="b1105-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b1105-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b1105-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b1105-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b1105-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b1105-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="b1105-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b1105-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="b1105-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b1105-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b1105-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="b1105-119">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b1105-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="b1105-120">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="b1105-120">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="b1105-121">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1105-121">Creates a Storage account.</span></span> |
| [<span data-ttu-id="b1105-122">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="b1105-122">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="b1105-123">設定資料庫的稽核原則。</span><span class="sxs-lookup"><span data-stu-id="b1105-123">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="b1105-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="b1105-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="b1105-125">設定資料庫的威脅偵測原則。</span><span class="sxs-lookup"><span data-stu-id="b1105-125">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="b1105-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b1105-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b1105-127">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="b1105-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b1105-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1105-128">Next steps</span></span>

<span data-ttu-id="b1105-129">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b1105-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b1105-130">其他的 SQL Database PowerShell 指令碼範例可於 [Azure SQL Database PowerShell 指令碼](../sql-database-powershell-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="b1105-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
