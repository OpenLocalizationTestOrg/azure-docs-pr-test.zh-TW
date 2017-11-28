---
title: "使用 PowerShell 的 Azure Analysis Services aaaManage |Microsoft 文件"
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
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a><span data-ttu-id="830cc-103">使用 PowerShell 管理 Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="830cc-103">Manage Azure Analysis Services with PowerShell</span></span>

<span data-ttu-id="830cc-104">本文說明的 PowerShell cmdlet 使用 tooperform Azure Analysis Services 伺服器和資料庫管理工作。</span><span class="sxs-lookup"><span data-stu-id="830cc-104">This article describes PowerShell cmdlets used tooperform Azure Analysis Services server and database management tasks.</span></span> 

<span data-ttu-id="830cc-105">伺服器管理工作，例如建立或刪除伺服器、 暫停或繼續伺服器作業，或變更 hello 服務層級 （層級） 會使用 Azure 資源管理員 (AzureRM) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="830cc-105">Server management tasks such as creating or deleting a server, suspending or resuming server operations, or changing hello service level (tier) use Azure Resource Manager (AzureRM) cmdlets.</span></span> <span data-ttu-id="830cc-106">管理資料庫，例如加入或移除角色成員、 處理或資料分割使用的 cmdlet 中包含的其他工作 hello 相同 SQL Server Analysis Services 的 SqlServer 模組。</span><span class="sxs-lookup"><span data-stu-id="830cc-106">Other tasks for managing databases such as adding or removing role members, processing, or partitioning use cmdlets included in hello same SqlServer module as SQL Server Analysis Services.</span></span>

## <a name="permissions"></a><span data-ttu-id="830cc-107">權限</span><span class="sxs-lookup"><span data-stu-id="830cc-107">Permissions</span></span>
<span data-ttu-id="830cc-108">大部分的 PowerShell 工作需要您所管理的 hello Analysis Services 伺服器上具有管理員權限。</span><span class="sxs-lookup"><span data-stu-id="830cc-108">Most PowerShell tasks require you have Admin privileges on hello Analysis Services server you are managing.</span></span> <span data-ttu-id="830cc-109">排定的 PowerShell 工作都是自動的作業。</span><span class="sxs-lookup"><span data-stu-id="830cc-109">Scheduled PowerShell tasks are unattended operations.</span></span> <span data-ttu-id="830cc-110">hello Analysis Services 伺服器上，執行 hello 排程器的 hello 帳戶必須具有系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="830cc-110">hello account running hello scheduler must have Admin privileges on hello Analysis Services server.</span></span> 

<span data-ttu-id="830cc-111">伺服器作業使用 AzureRm cmdlet，為您的帳戶或執行排程器的 hello 帳戶也必須屬於 toohello 擁有者角色中的 hello 資源[所有存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="830cc-111">For server operations using AzureRm cmdlets, your account or hello account running scheduler must also belong toohello Owner role for hello resource in [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> 

## <a name="server-operations"></a><span data-ttu-id="830cc-112">伺服器作業</span><span class="sxs-lookup"><span data-stu-id="830cc-112">Server operations</span></span> 
<span data-ttu-id="830cc-113">Azure Analysis Services 指令程式會包含在 hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)元件的模組。</span><span class="sxs-lookup"><span data-stu-id="830cc-113">Azure Analysis Services cmdlets are included in hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) component module.</span></span> <span data-ttu-id="830cc-114">tooinstall AzureRM cmdlet 模組，請參閱[Azure 資源管理員 cmdlet](/powershell/azure/overview) hello PowerShell 資源庫中。</span><span class="sxs-lookup"><span data-stu-id="830cc-114">tooinstall AzureRM cmdlet modules, see [Azure Resource Manager cmdlets](/powershell/azure/overview) in hello PowerShell Gallery.</span></span>

|<span data-ttu-id="830cc-115">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="830cc-115">Cmdlet</span></span>|<span data-ttu-id="830cc-116">說明</span><span class="sxs-lookup"><span data-stu-id="830cc-116">Description</span></span>| 
|------------|-----------------| 
|[<span data-ttu-id="830cc-117">Export-AzureAnalysisServicesInstance</span><span class="sxs-lookup"><span data-stu-id="830cc-117">Export-AzureAnalysisServicesInstance</span></span>](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|<span data-ttu-id="830cc-118">匯出記錄 toofile。</span><span class="sxs-lookup"><span data-stu-id="830cc-118">Exports log toofile.</span></span>| 
|[<span data-ttu-id="830cc-119">Get-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="830cc-119">Get-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|<span data-ttu-id="830cc-120">取得伺服器執行個體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="830cc-120">Gets details of a server instance.</span></span>|  
|[<span data-ttu-id="830cc-121">New-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="830cc-121">New-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|<span data-ttu-id="830cc-122">建立伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="830cc-122">Creates a server instance.</span></span>|
|[<span data-ttu-id="830cc-123">Remove-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="830cc-123">Remove-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|<span data-ttu-id="830cc-124">移除伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="830cc-124">Removes a server instance.</span></span>|  
|[<span data-ttu-id="830cc-125">Suspend-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="830cc-125">Suspend-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|<span data-ttu-id="830cc-126">暫停伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="830cc-126">Suspends a server instance.</span></span>| 
|[<span data-ttu-id="830cc-127">Resume-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="830cc-127">Resume-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|<span data-ttu-id="830cc-128">繼續伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="830cc-128">Resumes a server instance.</span></span>|  
|[<span data-ttu-id="830cc-129">Set-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="830cc-129">Set-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|<span data-ttu-id="830cc-130">修改伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="830cc-130">Modifies a server instance.</span></span>|   
|[<span data-ttu-id="830cc-131">Test-AzureRmAnalysisServicesServer</span><span class="sxs-lookup"><span data-stu-id="830cc-131">Test-AzureRmAnalysisServicesServer</span></span>](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|<span data-ttu-id="830cc-132">測試 hello 存在伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="830cc-132">Tests hello existence of a server  instance.</span></span>| 

## <a name="database-operations"></a><span data-ttu-id="830cc-133">資料庫作業</span><span class="sxs-lookup"><span data-stu-id="830cc-133">Database operations</span></span>

<span data-ttu-id="830cc-134">Azure Analysis Services 資料庫作業使用 hello 相同[SqlServer](https://www.powershellgallery.com/packages/SqlServer) SQL Server Analysis Services 的模組。</span><span class="sxs-lookup"><span data-stu-id="830cc-134">Azure Analysis Services database operations use hello same [SqlServer](https://www.powershellgallery.com/packages/SqlServer) module as SQL Server Analysis Services.</span></span> <span data-ttu-id="830cc-135">不過，Azure Analysis Services 並不支援所有的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="830cc-135">However, not all cmdlets are supported for Azure Analysis Services.</span></span> 

<span data-ttu-id="830cc-136">hello SqlServer 模組提供特定工作的資料庫管理指令程式以及 hello 一般用途 Invoke-ascmd 指令程式可接受表格式模型指令碼語言 」 (TMSL) 查詢或指令碼。</span><span class="sxs-lookup"><span data-stu-id="830cc-136">hello SqlServer module provides task-specific database management cmdlets as well as hello general purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="830cc-137">hello hello SqlServer 模組中的下列指令程式支援 Azure Analysis Services。</span><span class="sxs-lookup"><span data-stu-id="830cc-137">hello following cmdlets in hello SqlServer module are supported for Azure Analysis Services.</span></span>

  
|<span data-ttu-id="830cc-138">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="830cc-138">Cmdlet</span></span>|<span data-ttu-id="830cc-139">說明</span><span class="sxs-lookup"><span data-stu-id="830cc-139">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="830cc-140">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="830cc-140">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="830cc-141">加入成員 tooa 資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="830cc-141">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="830cc-142">Backup-ASDatabase</span><span class="sxs-lookup"><span data-stu-id="830cc-142">Backup-ASDatabase</span></span>](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|<span data-ttu-id="830cc-143">備份 Analysis Services 資料庫。</span><span class="sxs-lookup"><span data-stu-id="830cc-143">Backup an Analysis Services database.</span></span>|  
|[<span data-ttu-id="830cc-144">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="830cc-144">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="830cc-145">從資料庫角色移除成員。</span><span class="sxs-lookup"><span data-stu-id="830cc-145">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="830cc-146">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="830cc-146">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="830cc-147">執行 TMSL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="830cc-147">Execute a TMSL script.</span></span>|
|[<span data-ttu-id="830cc-148">Invoke-ProcessASDatabase</span><span class="sxs-lookup"><span data-stu-id="830cc-148">Invoke-ProcessASDatabase</span></span>](https://msdn.microsoft.com/library/mt651773.aspx)|<span data-ttu-id="830cc-149">處理資料庫。</span><span class="sxs-lookup"><span data-stu-id="830cc-149">Process a database.</span></span>|  
|[<span data-ttu-id="830cc-150">Invoke-ProcessPartition</span><span class="sxs-lookup"><span data-stu-id="830cc-150">Invoke-ProcessPartition</span></span>](https://msdn.microsoft.com/library/hh510164.aspx)|<span data-ttu-id="830cc-151">處理資料分割。</span><span class="sxs-lookup"><span data-stu-id="830cc-151">Process a partition.</span></span>| 
|[<span data-ttu-id="830cc-152">Invoke-ProcessTable</span><span class="sxs-lookup"><span data-stu-id="830cc-152">Invoke-ProcessTable</span></span>](https://msdn.microsoft.com/library/mt651774.aspx)|<span data-ttu-id="830cc-153">處理資料表。</span><span class="sxs-lookup"><span data-stu-id="830cc-153">Process a table.</span></span>|  
|[<span data-ttu-id="830cc-154">Merge-Partition</span><span class="sxs-lookup"><span data-stu-id="830cc-154">Merge-Partition</span></span>](https://msdn.microsoft.com/library/hh479576.aspx)|<span data-ttu-id="830cc-155">合併資料分割。</span><span class="sxs-lookup"><span data-stu-id="830cc-155">Merge a partition.</span></span>|  
|[<span data-ttu-id="830cc-156">Restore-ASDatabase</span><span class="sxs-lookup"><span data-stu-id="830cc-156">Restore-ASDatabase</span></span>](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|<span data-ttu-id="830cc-157">還原 Analysis Services 資料庫。</span><span class="sxs-lookup"><span data-stu-id="830cc-157">Restore an Analysis Services database.</span></span>| 
  

## <a name="related-information"></a><span data-ttu-id="830cc-158">相關資訊</span><span class="sxs-lookup"><span data-stu-id="830cc-158">Related information</span></span>

* [<span data-ttu-id="830cc-159">下載 SQL Server PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="830cc-159">Download SQL Server PowerShell Module</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [<span data-ttu-id="830cc-160">下載 SSMS</span><span class="sxs-lookup"><span data-stu-id="830cc-160">Download SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [<span data-ttu-id="830cc-161">PowerShell 資源庫中的 SqlServer 模組</span><span class="sxs-lookup"><span data-stu-id="830cc-161">SqlServer module in PowerShell Gallery</span></span>](https://www.powershellgallery.com/packages/SqlServer)    
* [<span data-ttu-id="830cc-162">相容性層級 1200 和更高層級的表格式模型程式設計</span><span class="sxs-lookup"><span data-stu-id="830cc-162">Tabular Model Programming for Compatibility Level 1200 and higher</span></span>](https://msdn.microsoft.com/library/mt712541.aspx)
