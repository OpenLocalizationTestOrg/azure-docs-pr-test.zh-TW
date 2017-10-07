---
title: "aaaAutomated 修補 SQL Server Vm （傳統） |Microsoft 文件"
description: "說明 hello 自動修補功能的 SQL Server 虛擬機器在 Azure 使用 hello 傳統部署模式中執行。"
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
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="e9419-103">Azure 虛擬機器中的 SQL Server 自動修補 (傳統)</span><span class="sxs-lookup"><span data-stu-id="e9419-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9419-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="e9419-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="e9419-105">傳統</span><span class="sxs-lookup"><span data-stu-id="e9419-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="e9419-106">自動修補會針對執行 SQL Server 的 Azure 虛擬機器建立維護時間範圍。</span><span class="sxs-lookup"><span data-stu-id="e9419-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="e9419-107">自動更新只能在此維護時間範圍內安裝。</span><span class="sxs-lookup"><span data-stu-id="e9419-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="e9419-108">針對 SQL Server，這可確保系統更新和任何相關聯的重新啟動發生在 hello 最佳時機進行 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e9419-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="e9419-109">自動的修補取決於 hello [SQL Server IaaS 代理程式延伸模組](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="e9419-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e9419-110">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="e9419-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e9419-111">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="e9419-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e9419-112">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="e9419-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e9419-113">請參閱這篇文章，tooview hello 資源管理員版本[自動修補 SQL server 在 Azure 虛擬機器資源管理員](../sql/virtual-machines-windows-sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="e9419-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9419-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="e9419-114">Prerequisites</span></span>
<span data-ttu-id="e9419-115">toouse 自動修補，請考慮下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="e9419-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="e9419-116">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="e9419-116">**Operating System**:</span></span>

* <span data-ttu-id="e9419-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e9419-117">Windows Server 2012</span></span>
* <span data-ttu-id="e9419-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e9419-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="e9419-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e9419-119">Windows Server 2016</span></span>

<span data-ttu-id="e9419-120">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="e9419-120">**SQL Server version**:</span></span>

* <span data-ttu-id="e9419-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="e9419-121">SQL Server 2012</span></span>
* <span data-ttu-id="e9419-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e9419-122">SQL Server 2014</span></span>
* <span data-ttu-id="e9419-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="e9419-123">SQL Server 2016</span></span>

<span data-ttu-id="e9419-124">**Azure PowerShell**：</span><span class="sxs-lookup"><span data-stu-id="e9419-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="e9419-125">[安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e9419-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="e9419-126">**SQL Server IaaS 擴充功能**：</span><span class="sxs-lookup"><span data-stu-id="e9419-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="e9419-127">[安裝 SQL Server IaaS 延伸模組 hello](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="e9419-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="e9419-128">設定</span><span class="sxs-lookup"><span data-stu-id="e9419-128">Settings</span></span>
<span data-ttu-id="e9419-129">hello 下表描述可以設定自動修補 」 的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="e9419-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="e9419-130">對於傳統的 Vm，您必須使用 PowerShell tooconfigure 這些設定。</span><span class="sxs-lookup"><span data-stu-id="e9419-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="e9419-131">設定</span><span class="sxs-lookup"><span data-stu-id="e9419-131">Setting</span></span> | <span data-ttu-id="e9419-132">可能的值</span><span class="sxs-lookup"><span data-stu-id="e9419-132">Possible values</span></span> | <span data-ttu-id="e9419-133">說明</span><span class="sxs-lookup"><span data-stu-id="e9419-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e9419-134">**自動修補**</span><span class="sxs-lookup"><span data-stu-id="e9419-134">**Automated Patching**</span></span> |<span data-ttu-id="e9419-135">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="e9419-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="e9419-136">啟用或停用 Azure 虛擬機器的自動修補。</span><span class="sxs-lookup"><span data-stu-id="e9419-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="e9419-137">**維護排程**</span><span class="sxs-lookup"><span data-stu-id="e9419-137">**Maintenance schedule**</span></span> |<span data-ttu-id="e9419-138">每天、星期一、星期二、星期三、星期四、星期五、星期六、星期日</span><span class="sxs-lookup"><span data-stu-id="e9419-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="e9419-139">下載並安裝虛擬機器的 Windows、 SQL Server 和 Microsoft 更新的 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="e9419-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="e9419-140">**維護開始時間**</span><span class="sxs-lookup"><span data-stu-id="e9419-140">**Maintenance start hour**</span></span> |<span data-ttu-id="e9419-141">0-24</span><span class="sxs-lookup"><span data-stu-id="e9419-141">0-24</span></span> |<span data-ttu-id="e9419-142">hello 本機的開始時間 tooupdate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9419-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="e9419-143">**維護時間範圍**</span><span class="sxs-lookup"><span data-stu-id="e9419-143">**Maintenance window duration**</span></span> |<span data-ttu-id="e9419-144">30-180</span><span class="sxs-lookup"><span data-stu-id="e9419-144">30-180</span></span> |<span data-ttu-id="e9419-145">hello 的分鐘數允許 toocomplete hello 下載和安裝更新。</span><span class="sxs-lookup"><span data-stu-id="e9419-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="e9419-146">**PATCH 類別**</span><span class="sxs-lookup"><span data-stu-id="e9419-146">**Patch Category**</span></span> |<span data-ttu-id="e9419-147">重要事項</span><span class="sxs-lookup"><span data-stu-id="e9419-147">Important</span></span> |<span data-ttu-id="e9419-148">hello 類別目錄更新 toodownload 及安裝。</span><span class="sxs-lookup"><span data-stu-id="e9419-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="e9419-149">使用 PowerShell 進行設定</span><span class="sxs-lookup"><span data-stu-id="e9419-149">Configuration with PowerShell</span></span>
<span data-ttu-id="e9419-150">在下列範例的 hello，PowerShell 會使用的 tooconfigure 自動修補現有的 SQL Server VM 上。</span><span class="sxs-lookup"><span data-stu-id="e9419-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="e9419-151">hello **New-azurevmsqlserverautopatchingconfig**命令會設定為 「 自動更新的新維護視窗。</span><span class="sxs-lookup"><span data-stu-id="e9419-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="e9419-152">根據此範例中，hello 下表描述 hello hello 目標 Azure VM 上的實際效果：</span><span class="sxs-lookup"><span data-stu-id="e9419-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="e9419-153">參數</span><span class="sxs-lookup"><span data-stu-id="e9419-153">Parameter</span></span> | <span data-ttu-id="e9419-154">效果</span><span class="sxs-lookup"><span data-stu-id="e9419-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="e9419-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="e9419-155">**DayOfWeek**</span></span> |<span data-ttu-id="e9419-156">在每個星期四安裝修補程式。</span><span class="sxs-lookup"><span data-stu-id="e9419-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="e9419-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="e9419-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="e9419-158">在上午 11:00 開始更新。</span><span class="sxs-lookup"><span data-stu-id="e9419-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="e9419-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="e9419-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="e9419-160">必須在 120 分鐘內安裝修補程式。</span><span class="sxs-lookup"><span data-stu-id="e9419-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="e9419-161">根據 hello 開始時間，他們必須完成 1:00 pm。</span><span class="sxs-lookup"><span data-stu-id="e9419-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="e9419-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="e9419-162">**PatchCategory**</span></span> |<span data-ttu-id="e9419-163">hello 這個參數只可以設定為 「 重要 」。</span><span class="sxs-lookup"><span data-stu-id="e9419-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="e9419-164">它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="e9419-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="e9419-165">toodisable 自動修補相同指令碼而不執行 hello hello-Enable 參數 toohello New-azurevmsqlserverautopatchingconfig。</span><span class="sxs-lookup"><span data-stu-id="e9419-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="e9419-166">為進行安裝，可能需要幾分鐘的時間 toodisable 自動修補。</span><span class="sxs-lookup"><span data-stu-id="e9419-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9419-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9419-167">Next steps</span></span>
<span data-ttu-id="e9419-168">如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="e9419-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="e9419-169">如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e9419-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

