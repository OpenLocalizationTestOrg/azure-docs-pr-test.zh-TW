---
title: "備份 SQL Server 2014 Azure 虛擬機器的 aaaAutomated |Microsoft 文件"
description: "用於在 Azure 中執行的 SQL Server 2014 Vm 說明 hello 自動備份功能。 本文是特定 tooVMs 使用 hello 資源管理員。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="eefa2-104">SQL Server 2014 虛擬機器的自動備份 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="eefa2-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eefa2-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="eefa2-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="eefa2-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="eefa2-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="eefa2-107">自動的備份會自動設定[Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx)執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM 上的所有現有和新資料庫。</span><span class="sxs-lookup"><span data-stu-id="eefa2-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="eefa2-108">這可讓您利用持久 Azure blob 儲存體的 tooconfigure 一般資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="eefa2-109">自動的備份取決於 hello [SQL Server IaaS 代理程式延伸模組](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="eefa2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="eefa2-110">Prerequisites</span></span>
<span data-ttu-id="eefa2-111">toouse 自動備份，請考慮下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="eefa2-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="eefa2-112">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="eefa2-112">**Operating System**:</span></span>

- <span data-ttu-id="eefa2-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="eefa2-113">Windows Server 2012</span></span>
- <span data-ttu-id="eefa2-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="eefa2-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="eefa2-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="eefa2-115">Windows Server 2016</span></span>

<span data-ttu-id="eefa2-116">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="eefa2-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="eefa2-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="eefa2-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="eefa2-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="eefa2-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eefa2-119">「自動備份」可與 SQL Server 2014 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="eefa2-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="eefa2-120">如果您使用 SQL Server 2016，您可以使用自動備份 v2 tooback 資料庫。</span><span class="sxs-lookup"><span data-stu-id="eefa2-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="eefa2-121">如需詳細資訊，請參閱 [SQL Server 2016 Azure 虛擬機器的自動備份 v2](virtual-machines-windows-sql-automated-backup-v2.md)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="eefa2-122">**資料庫組態**：</span><span class="sxs-lookup"><span data-stu-id="eefa2-122">**Database configuration**:</span></span>

- <span data-ttu-id="eefa2-123">目標資料庫必須使用 hello 完整復原模式。</span><span class="sxs-lookup"><span data-stu-id="eefa2-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="eefa2-124">如需詳細資訊 hello 影響 hello 完整復原模式的備份，請參閱[備份在 hello 完整復原模式](https://technet.microsoft.com/library/ms190217.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="eefa2-125">目標資料庫必須位於 hello 預設 SQL Server 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="eefa2-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="eefa2-126">hello SQL Server IaaS 延伸模組不支援具名執行個體。</span><span class="sxs-lookup"><span data-stu-id="eefa2-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="eefa2-127">**Azure 部署模型**：</span><span class="sxs-lookup"><span data-stu-id="eefa2-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="eefa2-128">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eefa2-128">Resource Manager</span></span>

<span data-ttu-id="eefa2-129">**Azure PowerShell**：</span><span class="sxs-lookup"><span data-stu-id="eefa2-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="eefa2-130">[安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)如果您計劃 tooconfigure 使用 PowerShell 的自動化備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="eefa2-131">自動的備份依賴 hello SQL Server IaaS 代理程式延伸模組。</span><span class="sxs-lookup"><span data-stu-id="eefa2-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="eefa2-132">目前的 SQL 虛擬機器資源庫映像預設會新增這項擴充。</span><span class="sxs-lookup"><span data-stu-id="eefa2-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="eefa2-133">如需詳細資訊，請參閱 [SQL Server IaaS 代理程式擴充](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="eefa2-134">設定</span><span class="sxs-lookup"><span data-stu-id="eefa2-134">Settings</span></span>

<span data-ttu-id="eefa2-135">hello 下表說明可以設定為自動備份的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="eefa2-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="eefa2-136">hello 實際的組態步驟，視您使用 hello Azure 入口網站或 Azure Windows PowerShell 命令而有所不同。</span><span class="sxs-lookup"><span data-stu-id="eefa2-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="eefa2-137">設定</span><span class="sxs-lookup"><span data-stu-id="eefa2-137">Setting</span></span> | <span data-ttu-id="eefa2-138">範圍 (預設值)</span><span class="sxs-lookup"><span data-stu-id="eefa2-138">Range (Default)</span></span> | <span data-ttu-id="eefa2-139">說明</span><span class="sxs-lookup"><span data-stu-id="eefa2-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eefa2-140">**自動備份**</span><span class="sxs-lookup"><span data-stu-id="eefa2-140">**Automated Backup**</span></span> | <span data-ttu-id="eefa2-141">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="eefa2-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="eefa2-142">針對執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM，啟用或停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="eefa2-143">**保留期限**</span><span class="sxs-lookup"><span data-stu-id="eefa2-143">**Retention Period**</span></span> | <span data-ttu-id="eefa2-144">1-30 天 (30 天)</span><span class="sxs-lookup"><span data-stu-id="eefa2-144">1-30 days (30 days)</span></span> | <span data-ttu-id="eefa2-145">hello 天 tooretain 備份數目。</span><span class="sxs-lookup"><span data-stu-id="eefa2-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="eefa2-146">**儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="eefa2-146">**Storage Account**</span></span> | <span data-ttu-id="eefa2-147">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="eefa2-147">Azure storage account</span></span> | <span data-ttu-id="eefa2-148">將自動備份檔案儲存在 blob 儲存體的 Azure 儲存體帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="eefa2-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="eefa2-149">所有備份檔案時，會在此位置 toostore 建立的容器。</span><span class="sxs-lookup"><span data-stu-id="eefa2-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="eefa2-150">hello 備份檔案命名慣例包括 hello 日期、 時間和電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="eefa2-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="eefa2-151">**加密**</span><span class="sxs-lookup"><span data-stu-id="eefa2-151">**Encryption**</span></span> | <span data-ttu-id="eefa2-152">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="eefa2-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="eefa2-153">啟用或停用加密。</span><span class="sxs-lookup"><span data-stu-id="eefa2-153">Enables or disables encryption.</span></span> <span data-ttu-id="eefa2-154">啟用加密時，在指定 hello 位於 hello 使用憑證 toorestore hello 備份儲存體帳戶中 hello 相同`automaticbackup`容器使用 hello 相同的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="eefa2-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="eefa2-155">如果 hello 密碼變更，與該密碼，產生新的憑證，但是 hello 舊的憑證會保留 toorestore 先前的備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="eefa2-156">**密碼**</span><span class="sxs-lookup"><span data-stu-id="eefa2-156">**Password**</span></span> | <span data-ttu-id="eefa2-157">密碼文字</span><span class="sxs-lookup"><span data-stu-id="eefa2-157">Password text</span></span> | <span data-ttu-id="eefa2-158">加密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="eefa2-158">A password for encryption keys.</span></span> <span data-ttu-id="eefa2-159">唯有啟用加密時，才需要此密碼。</span><span class="sxs-lookup"><span data-stu-id="eefa2-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="eefa2-160">順序 toorestore 中加密的備份，您必須擁有 hello 正確的密碼及相關的憑證所使用的 hello hello 備份執行的時間。</span><span class="sxs-lookup"><span data-stu-id="eefa2-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="eefa2-161">Hello 入口網站中的組態</span><span class="sxs-lookup"><span data-stu-id="eefa2-161">Configuration in hello Portal</span></span>

<span data-ttu-id="eefa2-162">在佈建期間，或用於現有的 SQL Server 2014 Vm，您可以使用 hello Azure 入口網站 tooconfigure 自動備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="eefa2-163">新的 VM</span><span class="sxs-lookup"><span data-stu-id="eefa2-163">New VMs</span></span>

<span data-ttu-id="eefa2-164">當您建立新的 SQL Server 2014 虛擬機器在 hello Resource Manager 部署模型時，請使用 hello Azure 入口網站 tooconfigure 自動備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="eefa2-165">在 hello **SQL Server 設定**刀鋒視窗中，選取**自動化備份**。</span><span class="sxs-lookup"><span data-stu-id="eefa2-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="eefa2-166">hello 下列 Azure 入口網站螢幕擷取畫面顯示 hello **SQL 自動備份**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="eefa2-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![在 Azure 入口網站中設定 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="eefa2-168">針對內容，請參閱 hello 完整主題[佈建 Azure 中的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="eefa2-169">現有的 VM</span><span class="sxs-lookup"><span data-stu-id="eefa2-169">Existing VMs</span></span>

<span data-ttu-id="eefa2-170">如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="eefa2-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="eefa2-171">然後選取 hello **SQL Server 組態**區段 hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="eefa2-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![現有 VM 的 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="eefa2-173">在 hello **SQL Server 組態**刀鋒視窗中，按一下 hello**編輯**hello 中的按鈕自動化備份 > 一節。</span><span class="sxs-lookup"><span data-stu-id="eefa2-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![設定現有 VM 的 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="eefa2-175">完成後，請按一下 hello **[確定]**上 hello hello 底部的按鈕**SQL Server 組態**刀鋒視窗 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="eefa2-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="eefa2-176">如果您要啟用自動備份 hello 第一次，Azure 會在 hello 背景設定 hello SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="eefa2-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="eefa2-177">在此期間，hello Azure 入口網站可能不會顯示已設定自動備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="eefa2-178">等待幾分鐘的時間安裝，hello 代理程式 toobe 設定。</span><span class="sxs-lookup"><span data-stu-id="eefa2-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="eefa2-179">之後的 hello Azure 入口網站將會反映 hello 新設定。</span><span class="sxs-lookup"><span data-stu-id="eefa2-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="eefa2-180">您也可以使用範本來設定「自動備份」。</span><span class="sxs-lookup"><span data-stu-id="eefa2-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="eefa2-181">如需詳細資訊，請參閱 [適用於自動備份的 Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="eefa2-182">使用 PowerShell 進行設定</span><span class="sxs-lookup"><span data-stu-id="eefa2-182">Configuration with PowerShell</span></span>

<span data-ttu-id="eefa2-183">您可以使用 PowerShell tooconfigure 自動備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="eefa2-184">開始進行之前，您必須：</span><span class="sxs-lookup"><span data-stu-id="eefa2-184">Before you begin, you must:</span></span>

- <span data-ttu-id="eefa2-185">[下載並安裝最新 Azure PowerShell 的 hello](http://aka.ms/webpi-azps)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="eefa2-186">開啟 Windows PowerShell 並將它與您的帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="eefa2-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="eefa2-187">您可以在 hello hello 步驟[設定您的訂用帳戶](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription)hello 佈建主題的章節。</span><span class="sxs-lookup"><span data-stu-id="eefa2-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="eefa2-188">安裝 hello SQL IaaS 延伸模組</span><span class="sxs-lookup"><span data-stu-id="eefa2-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="eefa2-189">如果您佈建 SQL Server 虛擬機器從 hello Azure 入口網站時，應該已安裝 hello SQL Server IaaS 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="eefa2-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="eefa2-190">您可以判斷是否它藉由呼叫安裝程式 vm **Get AzureRmVM**命令，並檢查 hello**延伸**屬性。</span><span class="sxs-lookup"><span data-stu-id="eefa2-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="eefa2-191">如果已安裝 hello SQL Server IaaS 代理程式延伸模組，您應該會看到它列為 「 SqlIaaSAgent"或"SQLIaaSExtension"。</span><span class="sxs-lookup"><span data-stu-id="eefa2-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="eefa2-192">**ProvisioningState** hello 延伸模組也應該顯示 「 成功 」。</span><span class="sxs-lookup"><span data-stu-id="eefa2-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="eefa2-193">如果未安裝或無法 toobe 佈建，您可以使用下列命令的 hello 來進行安裝。</span><span class="sxs-lookup"><span data-stu-id="eefa2-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="eefa2-194">在加法 toohello VM 名稱和資源群組中，您也必須指定 hello 區域 (**$region**) 中，位於您的 VM。</span><span class="sxs-lookup"><span data-stu-id="eefa2-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="eefa2-195"><a id="verifysettings"></a> 確認目前的設定</span><span class="sxs-lookup"><span data-stu-id="eefa2-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="eefa2-196">如果您在佈建期間啟用自動的備份，您可以使用 PowerShell toocheck 您目前的設定。</span><span class="sxs-lookup"><span data-stu-id="eefa2-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="eefa2-197">執行 hello **Get AzureRmVMSqlServerExtension**命令，並檢查 hello **AutoBackupSettings**屬性：</span><span class="sxs-lookup"><span data-stu-id="eefa2-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="eefa2-198">您應該取得類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="eefa2-198">You should get output similar toohello following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="eefa2-199">如果您的輸出顯示**啟用**設定得**False**，就會有 tooenable 自動的備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="eefa2-200">hello 好消息是您啟用並設定自動備份 hello 中相同的方式。</span><span class="sxs-lookup"><span data-stu-id="eefa2-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="eefa2-201">請參閱這項資訊的 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="eefa2-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="eefa2-202">如果您檢查 hello 設定進行變更後立即，很可能，您將會回到 hello 舊組態值。</span><span class="sxs-lookup"><span data-stu-id="eefa2-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="eefa2-203">等待幾分鐘的時間，並檢查 hello 設定一次 toomake 確定已套用的變更。</span><span class="sxs-lookup"><span data-stu-id="eefa2-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="eefa2-204">設定自動備份</span><span class="sxs-lookup"><span data-stu-id="eefa2-204">Configure Automated Backup</span></span>
<span data-ttu-id="eefa2-205">您可以使用 PowerShell tooenable 自動備份，以及 toomodify 其組態和行為在任何時間。</span><span class="sxs-lookup"><span data-stu-id="eefa2-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="eefa2-206">首先，選取或建立 hello 的儲存體帳戶的備份檔案。</span><span class="sxs-lookup"><span data-stu-id="eefa2-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="eefa2-207">hello 下列指令碼會選取儲存體帳戶，或建立如果不存在。</span><span class="sxs-lookup"><span data-stu-id="eefa2-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="eefa2-208">「自動備份」不支援將備份存放在進階儲存體中，但是可以從使用「進階儲存體」的 VM 磁碟進行備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="eefa2-209">然後使用 hello**新增 AzureRmVMSqlServerAutoBackupConfig**命令 tooenable 並設定 hello Azure 儲存體帳戶中的 hello 自動備份設定 toostore 備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="eefa2-210">在此範例中，hello 備份設定 toobe 保留 10 天。</span><span class="sxs-lookup"><span data-stu-id="eefa2-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="eefa2-211">hello 第二個命令，**組 AzureRmVMSqlServerExtension**，更新 hello Azure VM 指定這些設定。</span><span class="sxs-lookup"><span data-stu-id="eefa2-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="eefa2-212">它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="eefa2-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="eefa2-213">沒有其他設定**新增 AzureRmVMSqlServerAutoBackupConfig**套用只有 tooSQL Server 2016 和自動備份 v2。</span><span class="sxs-lookup"><span data-stu-id="eefa2-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="eefa2-214">SQL Server 2014 不支援下列設定的 hello: **BackupSystemDbs**， **BackupScheduleType**， **FullBackupFrequency**， **FullBackupStartHour**， **FullBackupWindowInHours**，和**LogBackupFrequencyInMinutes**。</span><span class="sxs-lookup"><span data-stu-id="eefa2-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="eefa2-215">如果您嘗試 tooconfigure SQL Server 2014 虛擬機器上的這些設定，沒有發生錯誤，但並不會套用 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="eefa2-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="eefa2-216">如果您想 toouse SQL Server 2016 的虛擬機器上的這些設定，請參閱[適用於 SQL Server 2016 Azure 虛擬機器的自動備份 v2](virtual-machines-windows-sql-automated-backup-v2.md)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="eefa2-217">tooenable 加密修改前一個指令碼 toopass hello hello **EnableEncryption**參數 hello 的密碼 （安全字串） 以及**CertificatePassword**參數。</span><span class="sxs-lookup"><span data-stu-id="eefa2-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="eefa2-218">hello 下列指令碼就會啟用 hello hello 前一個範例中的自動備份設定，並新增加密。</span><span class="sxs-lookup"><span data-stu-id="eefa2-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="eefa2-219">您的設定會套用，tooconfirm[確認 hello 自動備份組態](#verifysettings)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="eefa2-220">停用自動備份</span><span class="sxs-lookup"><span data-stu-id="eefa2-220">Disable Automated Backup</span></span>

<span data-ttu-id="eefa2-221">自動備份，執行相同指令碼沒有 hello 的 hello toodisable **-啟用**參數 toohello**新增 AzureRmVMSqlServerAutoBackupConfig**命令。</span><span class="sxs-lookup"><span data-stu-id="eefa2-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="eefa2-222">hello 缺乏 hello **-啟用**參數訊號 hello 命令 toodisable hello 功能。</span><span class="sxs-lookup"><span data-stu-id="eefa2-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="eefa2-223">如同安裝時，可能需要幾分鐘的時間 toodisable 自動備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="eefa2-224">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="eefa2-224">Example script</span></span>

<span data-ttu-id="eefa2-225">hello 下列指令碼提供一組變數，您可以自訂 tooenable 及設定自動備份您的 VM。</span><span class="sxs-lookup"><span data-stu-id="eefa2-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="eefa2-226">在您的情況下，您可能需要 toocustomize hello 指令碼，根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="eefa2-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="eefa2-227">例如，您會有 toomake 變更，如果您想 toodisable hello 系統資料庫備份，或啟用加密。</span><span class="sxs-lookup"><span data-stu-id="eefa2-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

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
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="eefa2-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eefa2-228">Next steps</span></span>

<span data-ttu-id="eefa2-229">自動備份會在 Azure VM 上設定受管理備份。</span><span class="sxs-lookup"><span data-stu-id="eefa2-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="eefa2-230">因此務必太[檢視 Managed Backup hello 文件](https://msdn.microsoft.com/library/dn449496.aspx)toounderstand hello 行為和影響。</span><span class="sxs-lookup"><span data-stu-id="eefa2-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="eefa2-231">您可以找到額外的備份和還原 Azure Vm 上的 SQL Server 的 hello 下列主題中的指導方針：[備份和還原 SQL server 在 Azure 虛擬機器](virtual-machines-windows-sql-backup-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="eefa2-232">如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](virtual-machines-windows-sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="eefa2-233">如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="eefa2-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

