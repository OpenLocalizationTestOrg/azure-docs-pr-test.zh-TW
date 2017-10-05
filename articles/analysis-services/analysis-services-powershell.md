---
title: "使用 PowerShell 管理 Azure Analysis Services | Microsoft Docs"
description: "使用 PowerShell 的 Azure Analysis Services 管理。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: 95593053950f96a83e093c29516e9f66ebad53bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a><span data-ttu-id="586b3-103">使用 PowerShell 管理 Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="586b3-103">Manage Azure Analysis Services with PowerShell</span></span>

<span data-ttu-id="586b3-104">本文說明用來執行 Azure Analysis Services 伺服器和資料庫管理工作的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="586b3-104">This article describes PowerShell cmdlets used to perform Azure Analysis Services server and database management tasks.</span></span> 

<span data-ttu-id="586b3-105">伺服器管理工作，例如建立或刪除伺服器、暫停或繼續伺服器作業，或是變更服務層級 (層級)，會使用 Azure Resource Manager (AzureRM) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="586b3-105">Server management tasks such as creating or deleting a server, suspending or resuming server operations, or changing the service level (tier) use Azure Resource Manager (AzureRM) cmdlets.</span></span> <span data-ttu-id="586b3-106">其他資料庫管理工作 (例如新增或移除角色成員、處理或資料分割) 會使用與 SQL Server Analysis Services 相同之 SqlServer 模組內含的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="586b3-106">Other tasks for managing databases such as adding or removing role members, processing, or partitioning use cmdlets included in the same SqlServer module as SQL Server Analysis Services.</span></span>

## <a name="permissions"></a><span data-ttu-id="586b3-107">權限</span><span class="sxs-lookup"><span data-stu-id="586b3-107">Permissions</span></span>
<span data-ttu-id="586b3-108">大部分的 PowerShell 工作需要您在您管理的 Analysis Services 伺服器上具備系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="586b3-108">Most PowerShell tasks require you have Admin privileges on the Analysis Services server you are managing.</span></span> <span data-ttu-id="586b3-109">排定的 PowerShell 工作都是自動的作業。</span><span class="sxs-lookup"><span data-stu-id="586b3-109">Scheduled PowerShell tasks are unattended operations.</span></span> <span data-ttu-id="586b3-110">執行排程器的帳戶必須具有 Analysis Services 伺服器上的管理員權限。</span><span class="sxs-lookup"><span data-stu-id="586b3-110">The account running the scheduler must have Admin privileges on the Analysis Services server.</span></span> 

<span data-ttu-id="586b3-111">針對使用 AzureRm Cmdlet 的伺服器作業，您的帳戶或執行排程器的帳戶也必須屬於 [Azure 角色型存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md) 中之資源的 Owner 角色。</span><span class="sxs-lookup"><span data-stu-id="586b3-111">For server operations using AzureRm cmdlets, your account or the account running scheduler must also belong to the Owner role for the resource in [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> 

## <a name="server-operations"></a><span data-ttu-id="586b3-112">伺服器作業</span><span class="sxs-lookup"><span data-stu-id="586b3-112">Server operations</span></span> 
<span data-ttu-id="586b3-113">Azure Analysis Services Cmdlet 包含在 [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) 元件模組中。</span><span class="sxs-lookup"><span data-stu-id="586b3-113">Azure Analysis Services cmdlets are included in the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) component module.</span></span> <span data-ttu-id="586b3-114">若要安裝 AzureRM Cmdlet 模組，請參閱 PowerShell 資源庫中的 [Azure Resource Manager Cmdlet (英文)](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="586b3-114">To install AzureRM cmdlet modules, see [Azure Resource Manager cmdlets](/powershell/azure/overview) in the PowerShell Gallery.</span></span>

|<span data-ttu-id="586b3-115">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="586b3-115">Cmdlet</span></span>|<span data-ttu-id="586b3-116">說明</span><span class="sxs-lookup"><span data-stu-id="586b3-116">Description</span></span>| 
|------------|-----------------| 
|[<span data-ttu-id="586b3-117">Export-AzureAnalysisServicesInstance</span><span class="sxs-lookup"><span data-stu-id="586b3-117">Export-AzureAnalysisServicesInstance</span></span>](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|<span data-ttu-id="586b3-118">將記錄匯出到檔案。</span><span class="sxs-lookup"><span data-stu-id="586b3-118">Exports log to file.</span></span>| 
|[<span data-ttu-id="586b3-119">Get-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="586b3-119">Get-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|<span data-ttu-id="586b3-120">取得伺服器執行個體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="586b3-120">Gets details of a server instance.</span></span>|  
|[<span data-ttu-id="586b3-121">New-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="586b3-121">New-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|<span data-ttu-id="586b3-122">建立伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="586b3-122">Creates a server instance.</span></span>|
|[<span data-ttu-id="586b3-123">Remove-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="586b3-123">Remove-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|<span data-ttu-id="586b3-124">移除伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="586b3-124">Removes a server instance.</span></span>|  
|[<span data-ttu-id="586b3-125">Suspend-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="586b3-125">Suspend-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|<span data-ttu-id="586b3-126">暫停伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="586b3-126">Suspends a server instance.</span></span>| 
|[<span data-ttu-id="586b3-127">Resume-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="586b3-127">Resume-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|<span data-ttu-id="586b3-128">繼續伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="586b3-128">Resumes a server instance.</span></span>|  
|[<span data-ttu-id="586b3-129">Set-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="586b3-129">Set-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|<span data-ttu-id="586b3-130">修改伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="586b3-130">Modifies a server instance.</span></span>|   
|[<span data-ttu-id="586b3-131">Test-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="586b3-131">Test-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|<span data-ttu-id="586b3-132">測試伺服器執行個體的存在。</span><span class="sxs-lookup"><span data-stu-id="586b3-132">Tests the existence of a server  instance.</span></span>| 

## <a name="database-operations"></a><span data-ttu-id="586b3-133">資料庫作業</span><span class="sxs-lookup"><span data-stu-id="586b3-133">Database operations</span></span>

<span data-ttu-id="586b3-134">Azure Analysis Services 資料庫作業會使用與 SQL Server Analysis Services 相同的 [SqlServer](https://www.powershellgallery.com/packages/SqlServer) 模組。</span><span class="sxs-lookup"><span data-stu-id="586b3-134">Azure Analysis Services database operations use the same [SqlServer](https://www.powershellgallery.com/packages/SqlServer) module as SQL Server Analysis Services.</span></span> <span data-ttu-id="586b3-135">不過，Azure Analysis Services 並不支援所有的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="586b3-135">However, not all cmdlets are supported for Azure Analysis Services.</span></span> 

<span data-ttu-id="586b3-136">SqlServer 模組提供特定工作的資料庫管理 Cmdlet，以及接受「表格式模型指令碼語言」(TMSL) 查詢或指令碼的一般用途 Invoke-ASCmd Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="586b3-136">The SqlServer module provides task-specific database management cmdlets as well as the general purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="586b3-137">Azure Analysis Services 支援 SqlServer 模組中的下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="586b3-137">The following cmdlets in the SqlServer module are supported for Azure Analysis Services.</span></span>

  
|<span data-ttu-id="586b3-138">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="586b3-138">Cmdlet</span></span>|<span data-ttu-id="586b3-139">說明</span><span class="sxs-lookup"><span data-stu-id="586b3-139">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="586b3-140">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="586b3-140">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="586b3-141">將成員新增到資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="586b3-141">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="586b3-142">Backup-ASDatabase</span><span class="sxs-lookup"><span data-stu-id="586b3-142">Backup-ASDatabase</span></span>](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|<span data-ttu-id="586b3-143">備份 Analysis Services 資料庫。</span><span class="sxs-lookup"><span data-stu-id="586b3-143">Backup an Analysis Services database.</span></span>|  
|[<span data-ttu-id="586b3-144">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="586b3-144">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="586b3-145">從資料庫角色移除成員。</span><span class="sxs-lookup"><span data-stu-id="586b3-145">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="586b3-146">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="586b3-146">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="586b3-147">執行 TMSL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="586b3-147">Execute a TMSL script.</span></span>|
|[<span data-ttu-id="586b3-148">Invoke-ProcessASDatabase</span><span class="sxs-lookup"><span data-stu-id="586b3-148">Invoke-ProcessASDatabase</span></span>](https://msdn.microsoft.com/library/mt651773.aspx)|<span data-ttu-id="586b3-149">處理資料庫。</span><span class="sxs-lookup"><span data-stu-id="586b3-149">Process a database.</span></span>|  
|[<span data-ttu-id="586b3-150">Invoke-ProcessPartition</span><span class="sxs-lookup"><span data-stu-id="586b3-150">Invoke-ProcessPartition</span></span>](https://msdn.microsoft.com/library/hh510164.aspx)|<span data-ttu-id="586b3-151">處理資料分割。</span><span class="sxs-lookup"><span data-stu-id="586b3-151">Process a partition.</span></span>| 
|[<span data-ttu-id="586b3-152">Invoke-ProcessTable</span><span class="sxs-lookup"><span data-stu-id="586b3-152">Invoke-ProcessTable</span></span>](https://msdn.microsoft.com/library/mt651774.aspx)|<span data-ttu-id="586b3-153">處理資料表。</span><span class="sxs-lookup"><span data-stu-id="586b3-153">Process a table.</span></span>|  
|[<span data-ttu-id="586b3-154">Merge-Partition</span><span class="sxs-lookup"><span data-stu-id="586b3-154">Merge-Partition</span></span>](https://msdn.microsoft.com/library/hh479576.aspx)|<span data-ttu-id="586b3-155">合併資料分割。</span><span class="sxs-lookup"><span data-stu-id="586b3-155">Merge a partition.</span></span>|  
|[<span data-ttu-id="586b3-156">Restore-ASDatabase</span><span class="sxs-lookup"><span data-stu-id="586b3-156">Restore-ASDatabase</span></span>](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|<span data-ttu-id="586b3-157">還原 Analysis Services 資料庫。</span><span class="sxs-lookup"><span data-stu-id="586b3-157">Restore an Analysis Services database.</span></span>| 
  

## <a name="related-information"></a><span data-ttu-id="586b3-158">相關資訊</span><span class="sxs-lookup"><span data-stu-id="586b3-158">Related information</span></span>

* [<span data-ttu-id="586b3-159">下載 SQL Server PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="586b3-159">Download SQL Server PowerShell Module</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [<span data-ttu-id="586b3-160">下載 SSMS</span><span class="sxs-lookup"><span data-stu-id="586b3-160">Download SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [<span data-ttu-id="586b3-161">PowerShell 資源庫中的 SqlServer 模組</span><span class="sxs-lookup"><span data-stu-id="586b3-161">SqlServer module in PowerShell Gallery</span></span>](https://www.powershellgallery.com/packages/SqlServer)    
* [<span data-ttu-id="586b3-162">相容性層級 1200 和更高層級的表格式模型程式設計</span><span class="sxs-lookup"><span data-stu-id="586b3-162">Tabular Model Programming for Compatibility Level 1200 and higher</span></span>](https://msdn.microsoft.com/library/mt712541.aspx)
