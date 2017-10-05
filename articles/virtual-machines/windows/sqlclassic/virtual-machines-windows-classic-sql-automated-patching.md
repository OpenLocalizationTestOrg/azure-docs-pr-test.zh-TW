---
title: "SQL Server VM 的自動修補 (傳統) | Microsoft Docs"
description: "針對 Azure 中以傳統部署模式執行的 SQL Server 虛擬機器，說明自動修補功能。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 1959871141f196ba80ffd7b37e62e5ea5b42dba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="d8679-103">Azure 虛擬機器中的 SQL Server 自動修補 (傳統)</span><span class="sxs-lookup"><span data-stu-id="d8679-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8679-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="d8679-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="d8679-105">傳統</span><span class="sxs-lookup"><span data-stu-id="d8679-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="d8679-106">自動修補會針對執行 SQL Server 的 Azure 虛擬機器建立維護時間範圍。</span><span class="sxs-lookup"><span data-stu-id="d8679-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="d8679-107">自動更新只能在此維護時間範圍內安裝。</span><span class="sxs-lookup"><span data-stu-id="d8679-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="d8679-108">對於 SQL Server，這可以確保系統更新和任何相關聯的重新啟動會在對資料庫最好的時間發生。</span><span class="sxs-lookup"><span data-stu-id="d8679-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="d8679-109">自動修補相依於 [SQL Server IaaS 代理程式擴充](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="d8679-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d8679-110">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d8679-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d8679-111">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="d8679-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d8679-112">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="d8679-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d8679-113">若要檢視這篇文章的 Resource Manager 版本，請參閱 [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md)(Azure 虛擬機器的 SQL Server 自動修補 (Resource Manager))。</span><span class="sxs-lookup"><span data-stu-id="d8679-113">To view the Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8679-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="d8679-114">Prerequisites</span></span>
<span data-ttu-id="d8679-115">若要使用自動修補，請考慮下列必要條件︰</span><span class="sxs-lookup"><span data-stu-id="d8679-115">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="d8679-116">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="d8679-116">**Operating System**:</span></span>

* <span data-ttu-id="d8679-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d8679-117">Windows Server 2012</span></span>
* <span data-ttu-id="d8679-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d8679-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="d8679-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d8679-119">Windows Server 2016</span></span>

<span data-ttu-id="d8679-120">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="d8679-120">**SQL Server version**:</span></span>

* <span data-ttu-id="d8679-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="d8679-121">SQL Server 2012</span></span>
* <span data-ttu-id="d8679-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="d8679-122">SQL Server 2014</span></span>
* <span data-ttu-id="d8679-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="d8679-123">SQL Server 2016</span></span>

<span data-ttu-id="d8679-124">**Azure PowerShell**：</span><span class="sxs-lookup"><span data-stu-id="d8679-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="d8679-125">[安裝最新的 Azure PowerShell 命令](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d8679-125">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="d8679-126">**SQL Server IaaS 擴充功能**：</span><span class="sxs-lookup"><span data-stu-id="d8679-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="d8679-127">[安裝 SQL Server IaaS 擴充功能](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="d8679-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="d8679-128">Settings</span><span class="sxs-lookup"><span data-stu-id="d8679-128">Settings</span></span>
<span data-ttu-id="d8679-129">下表說明可以為自動修補設定的選項。</span><span class="sxs-lookup"><span data-stu-id="d8679-129">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="d8679-130">針對傳統 VM，您必須使用 PowerShell 來設定這些設定。</span><span class="sxs-lookup"><span data-stu-id="d8679-130">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="d8679-131">設定</span><span class="sxs-lookup"><span data-stu-id="d8679-131">Setting</span></span> | <span data-ttu-id="d8679-132">可能的值</span><span class="sxs-lookup"><span data-stu-id="d8679-132">Possible values</span></span> | <span data-ttu-id="d8679-133">說明</span><span class="sxs-lookup"><span data-stu-id="d8679-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d8679-134">**自動修補**</span><span class="sxs-lookup"><span data-stu-id="d8679-134">**Automated Patching**</span></span> |<span data-ttu-id="d8679-135">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="d8679-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="d8679-136">啟用或停用 Azure 虛擬機器的自動修補。</span><span class="sxs-lookup"><span data-stu-id="d8679-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="d8679-137">**維護排程**</span><span class="sxs-lookup"><span data-stu-id="d8679-137">**Maintenance schedule**</span></span> |<span data-ttu-id="d8679-138">每天、星期一、星期二、星期三、星期四、星期五、星期六、星期日</span><span class="sxs-lookup"><span data-stu-id="d8679-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="d8679-139">虛擬機器的 Windows、SQL Server 和 Microsoft 更新的下載及安裝排程。</span><span class="sxs-lookup"><span data-stu-id="d8679-139">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="d8679-140">**維護開始時間**</span><span class="sxs-lookup"><span data-stu-id="d8679-140">**Maintenance start hour**</span></span> |<span data-ttu-id="d8679-141">0-24</span><span class="sxs-lookup"><span data-stu-id="d8679-141">0-24</span></span> |<span data-ttu-id="d8679-142">更新虛擬機器的當地開始時間。</span><span class="sxs-lookup"><span data-stu-id="d8679-142">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="d8679-143">**維護時間範圍**</span><span class="sxs-lookup"><span data-stu-id="d8679-143">**Maintenance window duration**</span></span> |<span data-ttu-id="d8679-144">30-180</span><span class="sxs-lookup"><span data-stu-id="d8679-144">30-180</span></span> |<span data-ttu-id="d8679-145">允許完成下載和安裝更新的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="d8679-145">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="d8679-146">**PATCH 類別**</span><span class="sxs-lookup"><span data-stu-id="d8679-146">**Patch Category**</span></span> |<span data-ttu-id="d8679-147">重要事項</span><span class="sxs-lookup"><span data-stu-id="d8679-147">Important</span></span> |<span data-ttu-id="d8679-148">要下載並安裝的更新類別。</span><span class="sxs-lookup"><span data-stu-id="d8679-148">The category of updates to download and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="d8679-149">使用 PowerShell 進行設定</span><span class="sxs-lookup"><span data-stu-id="d8679-149">Configuration with PowerShell</span></span>
<span data-ttu-id="d8679-150">在下列範例中，會使用 PowerShell 在現有的 SQL Server VM 上設定自動修補。</span><span class="sxs-lookup"><span data-stu-id="d8679-150">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="d8679-151">**New-AzureVMSqlServerAutoPatchingConfig** 命令會設定自動更新的維護時間範圍。</span><span class="sxs-lookup"><span data-stu-id="d8679-151">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="d8679-152">下表會根據此範例來描述對目標 Azure VM 的實際效果：</span><span class="sxs-lookup"><span data-stu-id="d8679-152">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="d8679-153">參數</span><span class="sxs-lookup"><span data-stu-id="d8679-153">Parameter</span></span> | <span data-ttu-id="d8679-154">效果</span><span class="sxs-lookup"><span data-stu-id="d8679-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="d8679-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="d8679-155">**DayOfWeek**</span></span> |<span data-ttu-id="d8679-156">在每個星期四安裝修補程式。</span><span class="sxs-lookup"><span data-stu-id="d8679-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="d8679-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="d8679-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="d8679-158">在上午 11:00 開始更新。</span><span class="sxs-lookup"><span data-stu-id="d8679-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="d8679-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="d8679-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="d8679-160">必須在 120 分鐘內安裝修補程式。</span><span class="sxs-lookup"><span data-stu-id="d8679-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="d8679-161">根據開始時間，其必須在下午 1:00 之前完成。</span><span class="sxs-lookup"><span data-stu-id="d8679-161">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="d8679-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="d8679-162">**PatchCategory**</span></span> |<span data-ttu-id="d8679-163">此參數唯一可能的設定是 "Important"。</span><span class="sxs-lookup"><span data-stu-id="d8679-163">The only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="d8679-164">可能需要幾分鐘的時間來安裝及設定 SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="d8679-164">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="d8679-165">若要停用自動修補，請執行相同的指令碼，但不要對 New-AzureVMSqlServerAutoPatchingConfig 使用 -Enable 參數。</span><span class="sxs-lookup"><span data-stu-id="d8679-165">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="d8679-166">和安裝一樣，可能需要幾分鐘的時間來停用自動修補。</span><span class="sxs-lookup"><span data-stu-id="d8679-166">As with installation, it can take several minutes to disable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8679-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8679-167">Next steps</span></span>
<span data-ttu-id="d8679-168">如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="d8679-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="d8679-169">如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d8679-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

