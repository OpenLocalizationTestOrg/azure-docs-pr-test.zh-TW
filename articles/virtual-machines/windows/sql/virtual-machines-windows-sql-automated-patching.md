---
title: "aaaAutomated 修補 SQL Server Vm （資源管理員） |Microsoft 文件"
description: "說明 hello 自動修補功能的 SQL Server 虛擬機器使用資源管理員在 Azure 中執行。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="1dd15-103">Azure 虛擬機器的 SQL Server 自動修補 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="1dd15-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1dd15-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="1dd15-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="1dd15-105">傳統</span><span class="sxs-lookup"><span data-stu-id="1dd15-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="1dd15-106">自動修補會針對執行 SQL Server 的 Azure 虛擬機器建立維護時間範圍。</span><span class="sxs-lookup"><span data-stu-id="1dd15-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="1dd15-107">自動更新只能在此維護時間範圍內安裝。</span><span class="sxs-lookup"><span data-stu-id="1dd15-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="1dd15-108">SQL Server 的這個 rescriction 可確保系統更新和任何相關聯的重新啟動發生在 hello 最佳時機進行 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1dd15-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="1dd15-109">自動的修補取決於 hello [SQL Server IaaS 代理程式延伸模組](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="1dd15-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="1dd15-110">tooview hello 精簡版本的本文中，請參閱[傳統 Azure 虛擬機器中的 SQL Server 自動修補](../classic/sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="1dd15-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dd15-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="1dd15-111">Prerequisites</span></span>
<span data-ttu-id="1dd15-112">toouse 自動修補，請考慮下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="1dd15-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="1dd15-113">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="1dd15-113">**Operating System**:</span></span>

* <span data-ttu-id="1dd15-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="1dd15-114">Windows Server 2012</span></span>
* <span data-ttu-id="1dd15-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1dd15-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="1dd15-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1dd15-116">Windows Server 2016</span></span>

<span data-ttu-id="1dd15-117">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="1dd15-117">**SQL Server version**:</span></span>

* <span data-ttu-id="1dd15-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="1dd15-118">SQL Server 2012</span></span>
* <span data-ttu-id="1dd15-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="1dd15-119">SQL Server 2014</span></span>
* <span data-ttu-id="1dd15-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="1dd15-120">SQL Server 2016</span></span>

<span data-ttu-id="1dd15-121">**Azure PowerShell**：</span><span class="sxs-lookup"><span data-stu-id="1dd15-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="1dd15-122">[安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)如果您計劃 tooconfigure 使用 PowerShell 自動修補。</span><span class="sxs-lookup"><span data-stu-id="1dd15-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="1dd15-123">自動的修補 」 依賴 hello SQL Server IaaS 代理程式延伸模組。</span><span class="sxs-lookup"><span data-stu-id="1dd15-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="1dd15-124">目前的 SQL 虛擬機器資源庫映像預設會新增這項擴充。</span><span class="sxs-lookup"><span data-stu-id="1dd15-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="1dd15-125">如需詳細資訊，請參閱 [SQL Server IaaS 代理程式擴充](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="1dd15-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="1dd15-126">設定</span><span class="sxs-lookup"><span data-stu-id="1dd15-126">Settings</span></span>
<span data-ttu-id="1dd15-127">hello 下表描述可以設定自動修補 」 的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="1dd15-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="1dd15-128">hello 實際的組態步驟，視您使用 hello Azure 入口網站或 Azure Windows PowerShell 命令而有所不同。</span><span class="sxs-lookup"><span data-stu-id="1dd15-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="1dd15-129">設定</span><span class="sxs-lookup"><span data-stu-id="1dd15-129">Setting</span></span> | <span data-ttu-id="1dd15-130">可能的值</span><span class="sxs-lookup"><span data-stu-id="1dd15-130">Possible values</span></span> | <span data-ttu-id="1dd15-131">說明</span><span class="sxs-lookup"><span data-stu-id="1dd15-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1dd15-132">**自動修補**</span><span class="sxs-lookup"><span data-stu-id="1dd15-132">**Automated Patching**</span></span> |<span data-ttu-id="1dd15-133">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="1dd15-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="1dd15-134">啟用或停用 Azure 虛擬機器的自動修補。</span><span class="sxs-lookup"><span data-stu-id="1dd15-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="1dd15-135">**維護排程**</span><span class="sxs-lookup"><span data-stu-id="1dd15-135">**Maintenance schedule**</span></span> |<span data-ttu-id="1dd15-136">每天、星期一、星期二、星期三、星期四、星期五、星期六、星期日</span><span class="sxs-lookup"><span data-stu-id="1dd15-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="1dd15-137">下載並安裝虛擬機器的 Windows、 SQL Server 和 Microsoft 更新的 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="1dd15-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="1dd15-138">**維護開始時間**</span><span class="sxs-lookup"><span data-stu-id="1dd15-138">**Maintenance start hour**</span></span> |<span data-ttu-id="1dd15-139">0-24</span><span class="sxs-lookup"><span data-stu-id="1dd15-139">0-24</span></span> |<span data-ttu-id="1dd15-140">hello 本機的開始時間 tooupdate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1dd15-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="1dd15-141">**維護時間範圍**</span><span class="sxs-lookup"><span data-stu-id="1dd15-141">**Maintenance window duration**</span></span> |<span data-ttu-id="1dd15-142">30-180</span><span class="sxs-lookup"><span data-stu-id="1dd15-142">30-180</span></span> |<span data-ttu-id="1dd15-143">hello 的分鐘數允許 toocomplete hello 下載和安裝更新。</span><span class="sxs-lookup"><span data-stu-id="1dd15-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="1dd15-144">**PATCH 類別**</span><span class="sxs-lookup"><span data-stu-id="1dd15-144">**Patch Category**</span></span> |<span data-ttu-id="1dd15-145">重要事項</span><span class="sxs-lookup"><span data-stu-id="1dd15-145">Important</span></span> |<span data-ttu-id="1dd15-146">hello 類別目錄更新 toodownload 及安裝。</span><span class="sxs-lookup"><span data-stu-id="1dd15-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="1dd15-147">Hello 入口網站中的組態</span><span class="sxs-lookup"><span data-stu-id="1dd15-147">Configuration in hello Portal</span></span>
<span data-ttu-id="1dd15-148">您可以使用 Azure 入口網站 tooconfigure hello 佈建期間，或現有 Vm 的自動修補。</span><span class="sxs-lookup"><span data-stu-id="1dd15-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="1dd15-149">新的 VM</span><span class="sxs-lookup"><span data-stu-id="1dd15-149">New VMs</span></span>
<span data-ttu-id="1dd15-150">使用 hello Azure 入口網站 tooconfigure hello Resource Manager 部署模型中建立新的 SQL Server 虛擬機器時自動修補。</span><span class="sxs-lookup"><span data-stu-id="1dd15-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="1dd15-151">在 hello **SQL Server 設定**刀鋒視窗中，選取**自動修補**。</span><span class="sxs-lookup"><span data-stu-id="1dd15-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="1dd15-152">hello 下列 Azure 入口網站螢幕擷取畫面顯示 hello **SQL 自動修補**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1dd15-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![Azure 入口網站中的 SQL 自動修補](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="1dd15-154">針對內容，請參閱 hello 完整主題[佈建 Azure 中的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="1dd15-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="1dd15-155">現有的 VM</span><span class="sxs-lookup"><span data-stu-id="1dd15-155">Existing VMs</span></span>
<span data-ttu-id="1dd15-156">如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1dd15-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="1dd15-157">然後選取 hello **SQL Server 組態**區段 hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1dd15-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![現有 VM 的 SQL 自動修補](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="1dd15-159">在 [hello **SQL Server 組態**刀鋒視窗中，按一下 hello**編輯**hello] 按鈕自動修補 > 一節。</span><span class="sxs-lookup"><span data-stu-id="1dd15-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![設定現有 VM 的 SQL 自動修補](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="1dd15-161">完成後，請按一下 hello **[確定]**上 hello hello 底部的按鈕**SQL Server 組態**刀鋒視窗 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="1dd15-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="1dd15-162">如果您要啟用自動修補 hello 第一次，Azure 會在 hello 背景設定 hello SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1dd15-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="1dd15-163">在此期間，hello Azure 入口網站可能不會顯示已設定自動修補。</span><span class="sxs-lookup"><span data-stu-id="1dd15-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="1dd15-164">等待幾分鐘的時間安裝，hello 代理程式 toobe 設定。</span><span class="sxs-lookup"><span data-stu-id="1dd15-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="1dd15-165">之後的 hello Azure 入口網站會反映 hello 新設定。</span><span class="sxs-lookup"><span data-stu-id="1dd15-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="1dd15-166">您也可以使用範本來設定「自動修補」。</span><span class="sxs-lookup"><span data-stu-id="1dd15-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="1dd15-167">如需詳細資訊，請參閱 [適用於自動修補的 Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update)。</span><span class="sxs-lookup"><span data-stu-id="1dd15-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="1dd15-168">使用 PowerShell 進行設定</span><span class="sxs-lookup"><span data-stu-id="1dd15-168">Configuration with PowerShell</span></span>
<span data-ttu-id="1dd15-169">佈建您的 SQL VM 之後, 使用 PowerShell tooconfigure 自動修補。</span><span class="sxs-lookup"><span data-stu-id="1dd15-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="1dd15-170">在下列範例的 hello，PowerShell 會使用的 tooconfigure 自動修補現有的 SQL Server VM 上。</span><span class="sxs-lookup"><span data-stu-id="1dd15-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="1dd15-171">hello **AzureRM.Compute\New New-azurevmsqlserverautopatchingconfig**命令會設定為 「 自動更新的新維護視窗。</span><span class="sxs-lookup"><span data-stu-id="1dd15-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="1dd15-172">根據此範例中，hello 下表描述 hello hello 目標 Azure VM 上的實際效果：</span><span class="sxs-lookup"><span data-stu-id="1dd15-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="1dd15-173">參數</span><span class="sxs-lookup"><span data-stu-id="1dd15-173">Parameter</span></span> | <span data-ttu-id="1dd15-174">效果</span><span class="sxs-lookup"><span data-stu-id="1dd15-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="1dd15-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="1dd15-175">**DayOfWeek**</span></span> |<span data-ttu-id="1dd15-176">在每個星期四安裝修補程式。</span><span class="sxs-lookup"><span data-stu-id="1dd15-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="1dd15-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="1dd15-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="1dd15-178">在上午 11:00 開始更新。</span><span class="sxs-lookup"><span data-stu-id="1dd15-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="1dd15-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="1dd15-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="1dd15-180">必須在 120 分鐘內安裝修補程式。</span><span class="sxs-lookup"><span data-stu-id="1dd15-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="1dd15-181">根據 hello 開始時間，他們必須完成 1:00 pm。</span><span class="sxs-lookup"><span data-stu-id="1dd15-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="1dd15-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="1dd15-182">**PatchCategory**</span></span> |<span data-ttu-id="1dd15-183">hello 唯一可能的設定此參數為**重要**。</span><span class="sxs-lookup"><span data-stu-id="1dd15-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="1dd15-184">它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1dd15-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="1dd15-185">toodisable 自動修補執行 hello 相同指令碼沒有 hello **-啟用**參數 toohello **AzureRM.Compute\New New-azurevmsqlserverautopatchingconfig**。</span><span class="sxs-lookup"><span data-stu-id="1dd15-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="1dd15-186">hello 缺乏 hello **-啟用**參數訊號 hello 命令 toodisable hello 功能。</span><span class="sxs-lookup"><span data-stu-id="1dd15-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dd15-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1dd15-187">Next steps</span></span>
<span data-ttu-id="1dd15-188">如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="1dd15-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="1dd15-189">如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1dd15-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

