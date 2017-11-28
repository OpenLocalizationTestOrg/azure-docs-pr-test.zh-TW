---
title: "aaaAutomated 備份 v2 適用於 SQL Server 2016 Azure 虛擬機器 |Microsoft 文件"
description: "用於在 Azure 中執行的 SQL Server 2016 Vm 說明 hello 自動備份功能。 本文是特定 tooVMs 使用 hello 資源管理員。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="7f575-104">SQL Server 2016 Azure 虛擬機器的自動備份 v2 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7f575-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f575-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="7f575-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="7f575-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="7f575-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="7f575-107">會自動設定自動的備份 v2 [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx)執行 SQL Server 2016 Standard、 Enterprise 或 Developer 版本的 Azure VM 上的所有現有和新資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f575-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="7f575-108">這可讓您利用持久 Azure blob 儲存體的 tooconfigure 一般資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="7f575-109">自動化的備份 v2 取決於 hello [SQL Server IaaS 代理程式延伸模組](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="7f575-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="7f575-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7f575-110">Prerequisites</span></span>
<span data-ttu-id="7f575-111">自動備份 v2 toouse 檢閱 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="7f575-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="7f575-112">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="7f575-112">**Operating System**:</span></span>

- <span data-ttu-id="7f575-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7f575-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="7f575-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7f575-114">Windows Server 2016</span></span>

<span data-ttu-id="7f575-115">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="7f575-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="7f575-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="7f575-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="7f575-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="7f575-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="7f575-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="7f575-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f575-119">「自動備份 v2」可與 SQL Server 2016 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="7f575-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="7f575-120">如果您使用 SQL Server 2014，您可以使用自動備份 v1 tooback 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f575-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="7f575-121">如需詳細資訊，請參閱 [SQL Server 2014 Azure 虛擬機器的自動備份](virtual-machines-windows-sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="7f575-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="7f575-122">**資料庫組態**：</span><span class="sxs-lookup"><span data-stu-id="7f575-122">**Database configuration**:</span></span>

- <span data-ttu-id="7f575-123">目標資料庫必須使用 hello 完整復原模式。</span><span class="sxs-lookup"><span data-stu-id="7f575-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="7f575-124">如需詳細資訊 hello 影響 hello 完整復原模式的備份，請參閱[備份在 hello 完整復原模式](https://technet.microsoft.com/library/ms190217.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7f575-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="7f575-125">系統資料庫沒有 toouse 完整復原模式。</span><span class="sxs-lookup"><span data-stu-id="7f575-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="7f575-126">不過，如果您需要記錄備份 toobe 所花費的模型或 MSDB，您必須使用完整復原模式。</span><span class="sxs-lookup"><span data-stu-id="7f575-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="7f575-127">目標資料庫必須位於 hello 預設 SQL Server 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="7f575-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="7f575-128">hello SQL Server IaaS 延伸模組不支援具名執行個體。</span><span class="sxs-lookup"><span data-stu-id="7f575-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="7f575-129">**Azure 部署模型**：</span><span class="sxs-lookup"><span data-stu-id="7f575-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="7f575-130">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7f575-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="7f575-131">自動的備份依賴 hello **SQL Server IaaS 代理程式延伸模組**。</span><span class="sxs-lookup"><span data-stu-id="7f575-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="7f575-132">目前的 SQL 虛擬機器資源庫映像預設會新增這項擴充。</span><span class="sxs-lookup"><span data-stu-id="7f575-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="7f575-133">如需詳細資訊，請參閱 [SQL Server IaaS 代理程式擴充](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="7f575-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="7f575-134">設定</span><span class="sxs-lookup"><span data-stu-id="7f575-134">Settings</span></span>
<span data-ttu-id="7f575-135">hello 下表說明可以設定自動備份 v2 的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="7f575-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="7f575-136">hello 實際的組態步驟，視您使用 hello Azure 入口網站或 Azure Windows PowerShell 命令而有所不同。</span><span class="sxs-lookup"><span data-stu-id="7f575-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="7f575-137">基本設定</span><span class="sxs-lookup"><span data-stu-id="7f575-137">Basic Settings</span></span>

| <span data-ttu-id="7f575-138">設定</span><span class="sxs-lookup"><span data-stu-id="7f575-138">Setting</span></span> | <span data-ttu-id="7f575-139">範圍 (預設值)</span><span class="sxs-lookup"><span data-stu-id="7f575-139">Range (Default)</span></span> | <span data-ttu-id="7f575-140">說明</span><span class="sxs-lookup"><span data-stu-id="7f575-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f575-141">**自動備份**</span><span class="sxs-lookup"><span data-stu-id="7f575-141">**Automated Backup**</span></span> | <span data-ttu-id="7f575-142">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="7f575-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="7f575-143">針對執行 SQL Server 2016 Standard 或 Enterprise 的 Azure VM，啟用或停用「自動備份」。</span><span class="sxs-lookup"><span data-stu-id="7f575-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="7f575-144">**保留期限**</span><span class="sxs-lookup"><span data-stu-id="7f575-144">**Retention Period**</span></span> | <span data-ttu-id="7f575-145">1-30 天 (30 天)</span><span class="sxs-lookup"><span data-stu-id="7f575-145">1-30 days (30 days)</span></span> | <span data-ttu-id="7f575-146">hello 天 tooretain 備份數目。</span><span class="sxs-lookup"><span data-stu-id="7f575-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="7f575-147">**儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="7f575-147">**Storage Account**</span></span> | <span data-ttu-id="7f575-148">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7f575-148">Azure storage account</span></span> | <span data-ttu-id="7f575-149">將自動備份檔案儲存在 blob 儲存體的 Azure 儲存體帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="7f575-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="7f575-150">所有備份檔案時，會在此位置 toostore 建立的容器。</span><span class="sxs-lookup"><span data-stu-id="7f575-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="7f575-151">hello 備份檔案命名慣例包括 hello 日期、 時間和資料庫的 GUID。</span><span class="sxs-lookup"><span data-stu-id="7f575-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="7f575-152">**加密**</span><span class="sxs-lookup"><span data-stu-id="7f575-152">**Encryption**</span></span> |<span data-ttu-id="7f575-153">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="7f575-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="7f575-154">啟用或停用加密。</span><span class="sxs-lookup"><span data-stu-id="7f575-154">Enables or disables encryption.</span></span> <span data-ttu-id="7f575-155">啟用加密時，在指定 hello 位於 hello 使用憑證 toorestore hello 備份儲存體帳戶中 hello 相同**automaticbackup**容器使用 hello 相同的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="7f575-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="7f575-156">如果 hello 密碼變更，與該密碼，產生新的憑證，但是 hello 舊的憑證會保留 toorestore 先前的備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="7f575-157">**密碼**</span><span class="sxs-lookup"><span data-stu-id="7f575-157">**Password**</span></span> |<span data-ttu-id="7f575-158">密碼文字</span><span class="sxs-lookup"><span data-stu-id="7f575-158">Password text</span></span> | <span data-ttu-id="7f575-159">加密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="7f575-159">A password for encryption keys.</span></span> <span data-ttu-id="7f575-160">唯有啟用加密時，才需要此密碼。</span><span class="sxs-lookup"><span data-stu-id="7f575-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="7f575-161">順序 toorestore 中加密的備份，您必須擁有 hello 正確的密碼及相關的憑證所使用的 hello hello 備份執行的時間。</span><span class="sxs-lookup"><span data-stu-id="7f575-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="7f575-162">進階設定</span><span class="sxs-lookup"><span data-stu-id="7f575-162">Advanced Settings</span></span>

| <span data-ttu-id="7f575-163">設定</span><span class="sxs-lookup"><span data-stu-id="7f575-163">Setting</span></span> | <span data-ttu-id="7f575-164">範圍 (預設值)</span><span class="sxs-lookup"><span data-stu-id="7f575-164">Range (Default)</span></span> | <span data-ttu-id="7f575-165">說明</span><span class="sxs-lookup"><span data-stu-id="7f575-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f575-166">**系統資料庫備份**</span><span class="sxs-lookup"><span data-stu-id="7f575-166">**System Database Backups**</span></span> | <span data-ttu-id="7f575-167">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="7f575-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="7f575-168">啟用時，這項功能也會備份 hello 系統資料庫： Master、 MSDB 和模型。</span><span class="sxs-lookup"><span data-stu-id="7f575-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="7f575-169">Hello MSDB 和 Model 資料庫，確認它們會在完整復原模式下，是否您想要採取的記錄檔備份 toobe。</span><span class="sxs-lookup"><span data-stu-id="7f575-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="7f575-170">針對 Master 是一律不進行記錄備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="7f575-171">而針對 TempDB 則不進行任何備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="7f575-172">**備份排程**</span><span class="sxs-lookup"><span data-stu-id="7f575-172">**Backup Schedule**</span></span> | <span data-ttu-id="7f575-173">手動/自動化 (自動化)</span><span class="sxs-lookup"><span data-stu-id="7f575-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="7f575-174">根據預設，hello 備份排程將會自動判斷根據 hello 記錄成長。</span><span class="sxs-lookup"><span data-stu-id="7f575-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="7f575-175">手動備份的排程可讓您備份 hello 使用者 toospecify hello 時間視窗。</span><span class="sxs-lookup"><span data-stu-id="7f575-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="7f575-176">在此情況下，備份將只會發生在 hello 指定頻率，且在 hello 期間的某一天的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="7f575-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="7f575-177">**完整備份頻率**</span><span class="sxs-lookup"><span data-stu-id="7f575-177">**Full backup frequency**</span></span> | <span data-ttu-id="7f575-178">每天/每週</span><span class="sxs-lookup"><span data-stu-id="7f575-178">Daily/Weekly</span></span> | <span data-ttu-id="7f575-179">完整備份的頻率。</span><span class="sxs-lookup"><span data-stu-id="7f575-179">Frequency of full backups.</span></span> <span data-ttu-id="7f575-180">在這兩種情況下，完整備份會開始在 hello 下一個排定的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="7f575-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="7f575-181">選取 [每週] 時，備份可以跨多天，直到所有資料庫都已順利備份為止。</span><span class="sxs-lookup"><span data-stu-id="7f575-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="7f575-182">**完整備份開始時間**</span><span class="sxs-lookup"><span data-stu-id="7f575-182">**Full backup start time**</span></span> | <span data-ttu-id="7f575-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="7f575-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="7f575-184">可進行完整備份的特定一天開始時間期間。</span><span class="sxs-lookup"><span data-stu-id="7f575-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="7f575-185">**完整備份時間範圍**</span><span class="sxs-lookup"><span data-stu-id="7f575-185">**Full backup time window**</span></span> | <span data-ttu-id="7f575-186">1 – 23 小時 (1 小時)</span><span class="sxs-lookup"><span data-stu-id="7f575-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="7f575-187">Hello 的某一天的完整備份便可以執行的時間間隔的持續時間。</span><span class="sxs-lookup"><span data-stu-id="7f575-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="7f575-188">**記錄備份頻率**</span><span class="sxs-lookup"><span data-stu-id="7f575-188">**Log backup frequency**</span></span> | <span data-ttu-id="7f575-189">5 – 60 分鐘 (60 分鐘)</span><span class="sxs-lookup"><span data-stu-id="7f575-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="7f575-190">記錄備份的頻率。</span><span class="sxs-lookup"><span data-stu-id="7f575-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="7f575-191">了解完整備份頻率</span><span class="sxs-lookup"><span data-stu-id="7f575-191">Understanding full backup frequency</span></span>
<span data-ttu-id="7f575-192">它會每日及每週完整備份的重要 toounderstand hello 差異。</span><span class="sxs-lookup"><span data-stu-id="7f575-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="7f575-193">為此，我們將逐步解說兩個範例案例。</span><span class="sxs-lookup"><span data-stu-id="7f575-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="7f575-194">案例 1：每週備份</span><span class="sxs-lookup"><span data-stu-id="7f575-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="7f575-195">您有一部包含一些非常大型資料庫的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="7f575-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="7f575-196">在星期一，您可以啟用自動備份 v2 以 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="7f575-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="7f575-197">備份排程：**自動**</span><span class="sxs-lookup"><span data-stu-id="7f575-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="7f575-198">完整備份頻率：**每週**</span><span class="sxs-lookup"><span data-stu-id="7f575-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="7f575-199">完整備份開始時間：**01:00**</span><span class="sxs-lookup"><span data-stu-id="7f575-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="7f575-200">完整備份時間範圍：**1 小時**</span><span class="sxs-lookup"><span data-stu-id="7f575-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="7f575-201">這表示該 hello 下一個可用備份時段星期二上午 1 小時 1。</span><span class="sxs-lookup"><span data-stu-id="7f575-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="7f575-202">到該時間，「自動備份」將開始逐一備份您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f575-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="7f575-203">在此案例中，您的資料庫已經很大完整備份將會完成的第一個幾資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="7f575-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="7f575-204">不過，在一小時後不是所有的 hello 資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="7f575-205">當發生這種情況時，就會開始自動備份，備份 hello 剩餘的資料庫 hello 隔天，星期三上午 1 小時 1。</span><span class="sxs-lookup"><span data-stu-id="7f575-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="7f575-206">如果並非所有的資料庫已在該時間備份，將會嘗試再次相同 hello hello 在隔天的時間。</span><span class="sxs-lookup"><span data-stu-id="7f575-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="7f575-207">這將會持續直到順利備份所有資料庫為止。</span><span class="sxs-lookup"><span data-stu-id="7f575-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="7f575-208">一旦再次到了星期二，「自動備份」就會重新開始再將所有資料庫都備份一遍。</span><span class="sxs-lookup"><span data-stu-id="7f575-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="7f575-209">此案例中會顯示自動備份只會在 hello 指定的時間視窗中，每個資料庫會備份每週的一次。</span><span class="sxs-lookup"><span data-stu-id="7f575-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="7f575-210">這也會顯示，有可能備份 toospan hello 中的多個天數的大小寫不可能 toocomplete 所有備份在一天。</span><span class="sxs-lookup"><span data-stu-id="7f575-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="7f575-211">案例 2：每天備份</span><span class="sxs-lookup"><span data-stu-id="7f575-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="7f575-212">您有一部包含一些非常大型資料庫的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="7f575-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="7f575-213">在星期一，您可以啟用自動備份 v2 以 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="7f575-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="7f575-214">備份排程：手動</span><span class="sxs-lookup"><span data-stu-id="7f575-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="7f575-215">完整備份頻率：每天</span><span class="sxs-lookup"><span data-stu-id="7f575-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="7f575-216">完整備份開始時間：22:00</span><span class="sxs-lookup"><span data-stu-id="7f575-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="7f575-217">完整備份時間範圍：6 小時</span><span class="sxs-lookup"><span data-stu-id="7f575-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="7f575-218">這表示該 hello 下一個可用備份時段星期一下午 10 點長達 6 小時。</span><span class="sxs-lookup"><span data-stu-id="7f575-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="7f575-219">到該時間，「自動備份」將開始逐一備份您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f575-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="7f575-220">然後，在星期二下午 10 點，將會重新開始進行所有資料庫的完整備份，持續時間為 6 小時。</span><span class="sxs-lookup"><span data-stu-id="7f575-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f575-221">當排定每日備份，建議您排程的所有資料庫都可以都備份此時間內寬時間視窗 tooensure。</span><span class="sxs-lookup"><span data-stu-id="7f575-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="7f575-222">這是最多有大量的資料 tooback hello 案例特別重要。</span><span class="sxs-lookup"><span data-stu-id="7f575-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="7f575-223">Hello 入口網站中的組態</span><span class="sxs-lookup"><span data-stu-id="7f575-223">Configuration in hello Portal</span></span>

<span data-ttu-id="7f575-224">您可以使用 hello Azure 入口網站 tooconfigure 自動備份 v2 期間佈建或現有的 SQL Server 2016 Vm。</span><span class="sxs-lookup"><span data-stu-id="7f575-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="7f575-225">新的 VM</span><span class="sxs-lookup"><span data-stu-id="7f575-225">New VMs</span></span>

<span data-ttu-id="7f575-226">當您建立新的 SQL Server 2016 虛擬機器在 hello Resource Manager 部署模型時，請使用 hello Azure 入口網站 tooconfigure 自動備份 v2。</span><span class="sxs-lookup"><span data-stu-id="7f575-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="7f575-227">在 hello **SQL Server 設定**刀鋒視窗中，選取**自動化備份**。</span><span class="sxs-lookup"><span data-stu-id="7f575-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="7f575-228">hello 下列 Azure 入口網站螢幕擷取畫面顯示 hello **SQL 自動備份**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7f575-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![在 Azure 入口網站中設定 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="7f575-230">預設會停用「自動備份 v2」。</span><span class="sxs-lookup"><span data-stu-id="7f575-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="7f575-231">針對內容，請參閱 hello 完整主題[佈建 Azure 中的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="7f575-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="7f575-232">現有的 VM</span><span class="sxs-lookup"><span data-stu-id="7f575-232">Existing VMs</span></span>

<span data-ttu-id="7f575-233">如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7f575-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="7f575-234">然後選取 hello **SQL Server 組態**區段 hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7f575-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![現有 VM 的 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="7f575-236">在 hello **SQL Server 組態**刀鋒視窗中，按一下 hello**編輯**hello 中的按鈕自動化備份 > 一節。</span><span class="sxs-lookup"><span data-stu-id="7f575-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![設定現有 VM 的 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="7f575-238">完成後，請按一下 hello **[確定]**上 hello hello 底部的按鈕**SQL Server 組態**刀鋒視窗 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="7f575-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="7f575-239">如果您要啟用自動備份 hello 第一次，Azure 會在 hello 背景設定 hello SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="7f575-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="7f575-240">在此期間，hello Azure 入口網站可能不會顯示已設定自動備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="7f575-241">等待幾分鐘的時間安裝，hello 代理程式 toobe 設定。</span><span class="sxs-lookup"><span data-stu-id="7f575-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="7f575-242">之後的 hello Azure 入口網站將會反映 hello 新設定。</span><span class="sxs-lookup"><span data-stu-id="7f575-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="7f575-243">使用 PowerShell 進行設定</span><span class="sxs-lookup"><span data-stu-id="7f575-243">Configuration with PowerShell</span></span>

<span data-ttu-id="7f575-244">您可以使用 PowerShell tooconfigure 自動備份 v2。</span><span class="sxs-lookup"><span data-stu-id="7f575-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="7f575-245">開始進行之前，您必須：</span><span class="sxs-lookup"><span data-stu-id="7f575-245">Before you begin, you must:</span></span>

- <span data-ttu-id="7f575-246">[下載並安裝最新 Azure PowerShell 的 hello](http://aka.ms/webpi-azps)。</span><span class="sxs-lookup"><span data-stu-id="7f575-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="7f575-247">開啟 Windows PowerShell 並將它與您的帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="7f575-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="7f575-248">您可以在 hello hello 步驟[設定您的訂用帳戶](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription)hello 佈建主題的章節。</span><span class="sxs-lookup"><span data-stu-id="7f575-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="7f575-249">安裝 hello SQL IaaS 延伸模組</span><span class="sxs-lookup"><span data-stu-id="7f575-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="7f575-250">如果您佈建 SQL Server 虛擬機器從 hello Azure 入口網站時，應該已安裝 hello SQL Server IaaS 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="7f575-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="7f575-251">您可以判斷是否它藉由呼叫安裝程式 vm **Get AzureRmVM**命令，並檢查 hello**延伸**屬性。</span><span class="sxs-lookup"><span data-stu-id="7f575-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="7f575-252">如果已安裝 hello SQL Server IaaS 代理程式延伸模組，您應該會看到它列為 「 SqlIaaSAgent"或"SQLIaaSExtension"。</span><span class="sxs-lookup"><span data-stu-id="7f575-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="7f575-253">**ProvisioningState** hello 延伸模組也應該顯示 「 成功 」。</span><span class="sxs-lookup"><span data-stu-id="7f575-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="7f575-254">如果未安裝或無法 toobe 佈建，您可以使用下列命令的 hello 來進行安裝。</span><span class="sxs-lookup"><span data-stu-id="7f575-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="7f575-255">在加法 toohello VM 名稱和資源群組中，您也必須指定 hello 區域 (**$region**) 中，位於您的 VM。</span><span class="sxs-lookup"><span data-stu-id="7f575-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="7f575-256"><a id="verifysettings"></a> 確認目前的設定</span><span class="sxs-lookup"><span data-stu-id="7f575-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="7f575-257">如果您在佈建期間啟用自動的備份，您可以使用 PowerShell toocheck 您目前的設定。</span><span class="sxs-lookup"><span data-stu-id="7f575-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="7f575-258">執行 hello **Get AzureRmVMSqlServerExtension**命令，並檢查 hello **AutoBackupSettings**屬性：</span><span class="sxs-lookup"><span data-stu-id="7f575-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="7f575-259">您應該取得類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="7f575-259">You should get output similar toohello following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="7f575-260">如果您的輸出顯示**啟用**設定得**False**，就會有 tooenable 自動的備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="7f575-261">hello 好消息是您啟用並設定自動備份 hello 中相同的方式。</span><span class="sxs-lookup"><span data-stu-id="7f575-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="7f575-262">請參閱這項資訊的 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="7f575-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="7f575-263">如果您檢查 hello 設定進行變更後立即，很可能，您將會回到 hello 舊組態值。</span><span class="sxs-lookup"><span data-stu-id="7f575-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="7f575-264">等待幾分鐘的時間，並檢查 hello 設定一次 toomake 確定已套用的變更。</span><span class="sxs-lookup"><span data-stu-id="7f575-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="7f575-265">設定自動備份 v2</span><span class="sxs-lookup"><span data-stu-id="7f575-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="7f575-266">您可以使用 PowerShell tooenable 自動備份，以及 toomodify 其組態和行為在任何時間。</span><span class="sxs-lookup"><span data-stu-id="7f575-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="7f575-267">首先，選取或建立 hello 的儲存體帳戶的備份檔案。</span><span class="sxs-lookup"><span data-stu-id="7f575-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="7f575-268">hello 下列指令碼會選取儲存體帳戶，或建立如果不存在。</span><span class="sxs-lookup"><span data-stu-id="7f575-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> <span data-ttu-id="7f575-269">「自動備份」不支援將備份存放在進階儲存體中，但是可以從使用「進階儲存體」的 VM 磁碟進行備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="7f575-270">然後使用 hello**新增 AzureRmVMSqlServerAutoBackupConfig**命令 tooenable 和 hello Azure 儲存體帳戶中設定自動備份 v2 hello 設定 toostore 備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="7f575-271">在此範例中，hello 備份設定 toobe 保留 10 天。</span><span class="sxs-lookup"><span data-stu-id="7f575-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="7f575-272">系統資料庫備份已啟用。</span><span class="sxs-lookup"><span data-stu-id="7f575-272">System database backups are enabled.</span></span> <span data-ttu-id="7f575-273">完整備份是排定為每週執行，時間範圍是從 20:00 開始並持續 2 小時。</span><span class="sxs-lookup"><span data-stu-id="7f575-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="7f575-274">記錄備份是排定為每 30 分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="7f575-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="7f575-275">hello 第二個命令，**組 AzureRmVMSqlServerExtension**，更新 hello Azure VM 指定這些設定。</span><span class="sxs-lookup"><span data-stu-id="7f575-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="7f575-276">它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="7f575-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="7f575-277">tooenable 加密修改前一個指令碼 toopass hello hello **EnableEncryption**參數 hello 的密碼 （安全字串） 以及**CertificatePassword**參數。</span><span class="sxs-lookup"><span data-stu-id="7f575-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="7f575-278">hello 下列指令碼就會啟用 hello hello 前一個範例中的自動備份設定，並新增加密。</span><span class="sxs-lookup"><span data-stu-id="7f575-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="7f575-279">您的設定會套用，tooconfirm[確認 hello 自動備份組態](#verifysettings)。</span><span class="sxs-lookup"><span data-stu-id="7f575-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="7f575-280">停用自動備份</span><span class="sxs-lookup"><span data-stu-id="7f575-280">Disable Automated Backup</span></span>
<span data-ttu-id="7f575-281">自動備份，執行相同指令碼沒有 hello 的 hello toodisable **-啟用**參數 toohello**新增 AzureRmVMSqlServerAutoBackupConfig**命令。</span><span class="sxs-lookup"><span data-stu-id="7f575-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="7f575-282">hello 缺乏 hello **-啟用**參數訊號 hello 命令 toodisable hello 功能。</span><span class="sxs-lookup"><span data-stu-id="7f575-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="7f575-283">如同安裝時，可能需要幾分鐘的時間 toodisable 自動備份。</span><span class="sxs-lookup"><span data-stu-id="7f575-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="7f575-284">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="7f575-284">Example script</span></span>
<span data-ttu-id="7f575-285">hello 下列指令碼提供一組變數，您可以自訂 tooenable 及設定自動備份您的 VM。</span><span class="sxs-lookup"><span data-stu-id="7f575-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="7f575-286">在您的情況下，您可能需要 toocustomize hello 指令碼，根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="7f575-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="7f575-287">例如，您會有 toomake 變更，如果您想 toodisable hello 系統資料庫備份，或啟用加密。</span><span class="sxs-lookup"><span data-stu-id="7f575-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="7f575-288">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f575-288">Next steps</span></span>
<span data-ttu-id="7f575-289">「自動備份 v2」會在 Azure VM 上設定 Managed Backup。</span><span class="sxs-lookup"><span data-stu-id="7f575-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="7f575-290">因此務必太[檢視 Managed Backup hello 文件](https://msdn.microsoft.com/library/dn449496.aspx)toounderstand hello 行為和影響。</span><span class="sxs-lookup"><span data-stu-id="7f575-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="7f575-291">您可以找到額外的備份和還原 Azure Vm 上的 SQL Server 的 hello 下列主題中的指導方針：[備份和還原 SQL server 在 Azure 虛擬機器](virtual-machines-windows-sql-backup-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="7f575-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="7f575-292">如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="7f575-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="7f575-293">如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7f575-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

