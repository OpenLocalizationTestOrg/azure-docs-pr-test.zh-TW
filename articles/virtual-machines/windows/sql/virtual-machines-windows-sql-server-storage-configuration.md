---
title: "SQL Server Vm 的 aaaStorage 組態 |Microsoft 文件"
description: "本主題說明 Azure 如何在佈建期間針對 SQL Server VM 設定儲存體 (Resource Manager 部署模型)。 它也會說明如何針對現有的 SQL Server VM 設定儲存體。"
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a><span data-ttu-id="3bced-104">SQL Server VM 的儲存體組態</span><span class="sxs-lookup"><span data-stu-id="3bced-104">Storage configuration for SQL Server VMs</span></span>
<span data-ttu-id="3bced-105">當您在 Azure 中設定 SQL Server 虛擬機器映像時，hello 入口網站可協助 tooautomate 存放裝置設定。</span><span class="sxs-lookup"><span data-stu-id="3bced-105">When you configure a SQL Server virtual machine image in Azure, hello Portal helps tooautomate your storage configuration.</span></span> <span data-ttu-id="3bced-106">這包括附加儲存體 toohello VM，讓該存放裝置可存取 tooSQL 伺服器，並將它設定為 toooptimize 適合您特定的效能需求。</span><span class="sxs-lookup"><span data-stu-id="3bced-106">This includes attaching storage toohello VM, making that storage accessible tooSQL Server, and configuring it toooptimize for your specific performance requirements.</span></span>

<span data-ttu-id="3bced-107">本主題說明 Azure 如何在佈建期間針對 SQL Server VM 及針對現有的 VM 設定儲存體。</span><span class="sxs-lookup"><span data-stu-id="3bced-107">This topic explains how Azure configures storage for your SQL Server VMs both during provisioning and for existing VMs.</span></span> <span data-ttu-id="3bced-108">此設定根據 hello[效能最佳做法](virtual-machines-windows-sql-performance.md)執行 SQL Server 的 Azure vm。</span><span class="sxs-lookup"><span data-stu-id="3bced-108">This configuration is based on hello [performance best practices](virtual-machines-windows-sql-performance.md) for Azure VMs running SQL Server.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="3bced-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="3bced-109">Prerequisites</span></span>
<span data-ttu-id="3bced-110">toouse hello 自動儲存組態設定，您的虛擬機器需要 hello 下列特性：</span><span class="sxs-lookup"><span data-stu-id="3bced-110">toouse hello automated storage configuration settings, your virtual machine requires hello following characteristics:</span></span>

* <span data-ttu-id="3bced-111">使用 [SQL Server 資源庫映像](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing)佈建。</span><span class="sxs-lookup"><span data-stu-id="3bced-111">Provisioned with a [SQL Server gallery image](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).</span></span>
* <span data-ttu-id="3bced-112">使用 hello [Resource Manager 部署模型](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3bced-112">Uses hello [Resource Manager deployment model](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="3bced-113">使用 [進階儲存體](../../../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="3bced-113">Uses [Premium Storage](../../../storage/common/storage-premium-storage.md).</span></span>

## <a name="new-vms"></a><span data-ttu-id="3bced-114">新的 VM</span><span class="sxs-lookup"><span data-stu-id="3bced-114">New VMs</span></span>
<span data-ttu-id="3bced-115">hello 下列各節說明如何為新的 SQL Server 虛擬機器的 tooconfigure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="3bced-115">hello following sections describe how tooconfigure storage for new SQL Server virtual machines.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="3bced-116">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3bced-116">Azure Portal</span></span>
<span data-ttu-id="3bced-117">當佈建 Azure VM 使用 SQL Server 資源庫映像，您可以選擇 tooautomatically 設定 hello 儲存新的 vm。</span><span class="sxs-lookup"><span data-stu-id="3bced-117">When provisioning an Azure VM using a SQL Server gallery image, you can choose tooautomatically configure hello storage for your new VM.</span></span> <span data-ttu-id="3bced-118">指定 hello 儲存體大小、 效能限制，以及工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="3bced-118">You specify hello storage size, performance limits, and workload type.</span></span> <span data-ttu-id="3bced-119">hello 下列螢幕擷取畫面顯示 hello 儲存體組態刀鋒視窗中的 SQL VM 期間使用佈建。</span><span class="sxs-lookup"><span data-stu-id="3bced-119">hello following screenshot shows hello Storage configuration blade used during SQL VM provisioning.</span></span>

![佈建期間的 SQL Server VM 儲存體設定](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

<span data-ttu-id="3bced-121">根據您的選擇，Azure 會執行下列存放裝置設定工作之後建立 hello VM hello:</span><span class="sxs-lookup"><span data-stu-id="3bced-121">Based on your choices, Azure performs hello following storage configuration tasks after creating hello VM:</span></span>

* <span data-ttu-id="3bced-122">建立並附加 premium 儲存體的資料磁碟 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3bced-122">Creates and attaches premium storage data disks toohello virtual machine.</span></span>
* <span data-ttu-id="3bced-123">設定 hello 資料磁碟 toobe 存取 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3bced-123">Configures hello data disks toobe accessible tooSQL Server.</span></span>
* <span data-ttu-id="3bced-124">設定 hello 資料磁碟到儲存體集區根據 hello 指定大小和效能 （IOPS 及輸送量） 的需求。</span><span class="sxs-lookup"><span data-stu-id="3bced-124">Configures hello data disks into a storage pool based on hello specified size and performance (IOPS and throughput) requirements.</span></span>
* <span data-ttu-id="3bced-125">將 hello 存放集區與 hello 虛擬機器上的新磁碟機產生關聯。</span><span class="sxs-lookup"><span data-stu-id="3bced-125">Associates hello storage pool with a new drive on hello virtual machine.</span></span>
* <span data-ttu-id="3bced-126">根據您指定的工作負載類型 (資料倉儲、交易式處理或一般)，最佳化這個新的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="3bced-126">Optimizes this new drive based on your specified workload type (Data warehousing, Transactional processing, or General).</span></span>

<span data-ttu-id="3bced-127">如需有關 Azure 會儲存設定的設定，請參閱 hello[儲存體組態區段](#storage-configuration)。</span><span class="sxs-lookup"><span data-stu-id="3bced-127">For further details on how Azure configures storage settings, see hello [Storage configuration section](#storage-configuration).</span></span> <span data-ttu-id="3bced-128">如需完整的逐步解說如何 toocreate hello Azure 入口網站中的 SQL Server VM 看到的[佈建教學課程中的 hello](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="3bced-128">For a full walkthrough of how toocreate a SQL Server VM in hello Azure Portal, see [hello provisioning tutorial](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="resource-manage-templates"></a><span data-ttu-id="3bced-129">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3bced-129">Resource Manage templates</span></span>
<span data-ttu-id="3bced-130">如果您使用下列資源管理員範本 hello，兩個高階資料磁碟附加根據預設，不需要儲存體集區組態。</span><span class="sxs-lookup"><span data-stu-id="3bced-130">If you use hello following Resource Manager templates, two premium data disks are attached by default, with no storage pool configuration.</span></span> <span data-ttu-id="3bced-131">不過，您可以自訂這些範本 toochange hello 的高階資料磁碟數目的附加的 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3bced-131">However, you can customize these templates toochange hello number of premium data disks that are attached toohello virtual machine.</span></span>

* [<span data-ttu-id="3bced-132">使用自動備份建立 VM</span><span class="sxs-lookup"><span data-stu-id="3bced-132">Create VM with Automated Backup</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [<span data-ttu-id="3bced-133">使用自動修補建立 VM</span><span class="sxs-lookup"><span data-stu-id="3bced-133">Create VM with Automated Patching</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [<span data-ttu-id="3bced-134">使用自 AKV 整合建立 VM</span><span class="sxs-lookup"><span data-stu-id="3bced-134">Create VM with AKV Integration</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a><span data-ttu-id="3bced-135">現有的 VM</span><span class="sxs-lookup"><span data-stu-id="3bced-135">Existing VMs</span></span>
<span data-ttu-id="3bced-136">對於現有 SQL Server Vm，您可以修改某些 hello Azure 入口網站中的儲存體設定。</span><span class="sxs-lookup"><span data-stu-id="3bced-136">For existing SQL Server VMs, you can modify some storage settings in hello Azure portal.</span></span> <span data-ttu-id="3bced-137">選取您的 VM，請 toohello 設定] 區域中，然後選取 [SQL Server 組態。</span><span class="sxs-lookup"><span data-stu-id="3bced-137">Select your VM, go toohello Settings area, and then select SQL Server Configuration.</span></span> <span data-ttu-id="3bced-138">hello SQL Server 組態刀鋒視窗會顯示您的 VM hello 目前儲存體使用量。</span><span class="sxs-lookup"><span data-stu-id="3bced-138">hello SQL Server Configuration blade shows hello current storage usage of your VM.</span></span> <span data-ttu-id="3bced-139">下圖顯示您的 VM 上存在的所有磁碟機。</span><span class="sxs-lookup"><span data-stu-id="3bced-139">All drives that exist on your VM are displayed in this chart.</span></span> <span data-ttu-id="3bced-140">每個磁碟機，hello 儲存空間會顯示四個區段：</span><span class="sxs-lookup"><span data-stu-id="3bced-140">For each drive, hello storage space displays in four sections:</span></span>

* <span data-ttu-id="3bced-141">SQL 資料</span><span class="sxs-lookup"><span data-stu-id="3bced-141">SQL data</span></span>
* <span data-ttu-id="3bced-142">SQL 記錄檔</span><span class="sxs-lookup"><span data-stu-id="3bced-142">SQL log</span></span>
* <span data-ttu-id="3bced-143">其他 (非 SQL 儲存體)</span><span class="sxs-lookup"><span data-stu-id="3bced-143">Other (non-SQL storage)</span></span>
* <span data-ttu-id="3bced-144">可用</span><span class="sxs-lookup"><span data-stu-id="3bced-144">Available</span></span>

![設定現有 SQL Server VM 的儲存體](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

<span data-ttu-id="3bced-146">tooconfigure hello 儲存體 tooadd 新磁碟機或擴充現有的磁碟機，按一下 hello hello 圖表之上的編輯連結。</span><span class="sxs-lookup"><span data-stu-id="3bced-146">tooconfigure hello storage tooadd a new drive or extend an existing drive, click hello Edit link above hello chart.</span></span>

<span data-ttu-id="3bced-147">您會看到您是否使用之前的這項功能而異的 hello 組態選項。</span><span class="sxs-lookup"><span data-stu-id="3bced-147">hello configuration options that you see varies depending on whether you have used this feature before.</span></span> <span data-ttu-id="3bced-148">當使用 hello 第一次，您可以指定新的磁碟機的儲存需求。</span><span class="sxs-lookup"><span data-stu-id="3bced-148">When using for hello first time, you can specify your storage requirements for a new drive.</span></span> <span data-ttu-id="3bced-149">如果您先前使用此功能 toocreate 磁碟機，您可以選擇 tooextend 該磁碟機的儲存體。</span><span class="sxs-lookup"><span data-stu-id="3bced-149">If you previously used this feature toocreate a drive, you can choose tooextend that drive’s storage.</span></span>

### <a name="use-for-hello-first-time"></a><span data-ttu-id="3bced-150">Hello 第一次使用</span><span class="sxs-lookup"><span data-stu-id="3bced-150">Use for hello first time</span></span>
<span data-ttu-id="3bced-151">如果是您第一次使用這項功能，您可以指定 hello 新磁碟機的儲存體大小和效能限制。</span><span class="sxs-lookup"><span data-stu-id="3bced-151">If it is your first time using this feature, you can specify hello storage size and performance limits for a new drive.</span></span> <span data-ttu-id="3bced-152">此體驗會是您在佈建時間將會看到類似 toowhat。</span><span class="sxs-lookup"><span data-stu-id="3bced-152">This experience is similar toowhat you would see at provisioning time.</span></span> <span data-ttu-id="3bced-153">hello 主要差異是不允許 toospecify hello 工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="3bced-153">hello main difference is that you are not permitted toospecify hello workload type.</span></span> <span data-ttu-id="3bced-154">這項限制可避免中斷 hello 虛擬機器上任何現有的 SQL Server 組態。</span><span class="sxs-lookup"><span data-stu-id="3bced-154">This restriction prevents disrupting any existing SQL Server configurations on hello virtual machine.</span></span>

![設定 SQL Server 儲存體滑桿](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

<span data-ttu-id="3bced-156">Azure 會根據您的規格建立新的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="3bced-156">Azure creates a new drive based on your specifications.</span></span> <span data-ttu-id="3bced-157">在此案例中，Azure 會執行下列存放裝置設定工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="3bced-157">In this scenario, Azure performs hello following storage configuration tasks:</span></span>

* <span data-ttu-id="3bced-158">建立並附加 premium 儲存體的資料磁碟 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3bced-158">Creates and attaches premium storage data disks toohello virtual machine.</span></span>
* <span data-ttu-id="3bced-159">設定 hello 資料磁碟 toobe 存取 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3bced-159">Configures hello data disks toobe accessible tooSQL Server.</span></span>
* <span data-ttu-id="3bced-160">設定 hello 資料磁碟到儲存體集區根據 hello 指定大小和效能 （IOPS 及輸送量） 的需求。</span><span class="sxs-lookup"><span data-stu-id="3bced-160">Configures hello data disks into a storage pool based on hello specified size and performance (IOPS and throughput) requirements.</span></span>
* <span data-ttu-id="3bced-161">將 hello 存放集區與 hello 虛擬機器上的新磁碟機產生關聯。</span><span class="sxs-lookup"><span data-stu-id="3bced-161">Associates hello storage pool with a new drive on hello virtual machine.</span></span>

<span data-ttu-id="3bced-162">如需有關 Azure 會儲存設定的設定，請參閱 hello[儲存體組態區段](#storage-configuration)。</span><span class="sxs-lookup"><span data-stu-id="3bced-162">For further details on how Azure configures storage settings, see hello [Storage configuration section](#storage-configuration).</span></span>

### <a name="add-a-new-drive"></a><span data-ttu-id="3bced-163">加入新的磁碟機</span><span class="sxs-lookup"><span data-stu-id="3bced-163">Add a new drive</span></span>
<span data-ttu-id="3bced-164">如果您已在 SQL Server VM 上設定儲存體，展開儲存體會顯示兩個新選項。</span><span class="sxs-lookup"><span data-stu-id="3bced-164">If you have already configured storage on your SQL Server VM, expanding storage brings up two new options.</span></span> <span data-ttu-id="3bced-165">hello 第一個選項是 tooadd 新的磁碟機，可以提高您的 VM hello 效能層級。</span><span class="sxs-lookup"><span data-stu-id="3bced-165">hello first option is tooadd a new drive, which can increase hello performance level of your VM.</span></span>

![加入新的磁碟機 tooa SQL VM](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

<span data-ttu-id="3bced-167">不過，加入之後 hello 磁碟機，您必須執行一些額外的手動組態 tooachieve hello 提升效能。</span><span class="sxs-lookup"><span data-stu-id="3bced-167">However, after adding hello drive, you must perform some extra manual configuration tooachieve hello performance increase.</span></span>

### <a name="extend-hello-drive"></a><span data-ttu-id="3bced-168">擴充 hello 磁碟機</span><span class="sxs-lookup"><span data-stu-id="3bced-168">Extend hello drive</span></span>
<span data-ttu-id="3bced-169">hello 擴充儲存體的其他選項為 tooextend hello 現有的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="3bced-169">hello other option for expanding storage is tooextend hello existing drive.</span></span> <span data-ttu-id="3bced-170">此選項會增加您的磁碟機的 hello 可用的存放裝置，但不會提高效能。</span><span class="sxs-lookup"><span data-stu-id="3bced-170">This option increases hello available storage for your drive, but it does not increase performance.</span></span> <span data-ttu-id="3bced-171">使用儲存集區，您無法在 hello 存放集區建立之後改變 hello 的資料行的數目。</span><span class="sxs-lookup"><span data-stu-id="3bced-171">With storage pools, you cannot alter hello number of columns after hello storage pool is created.</span></span> <span data-ttu-id="3bced-172">資料行的 hello 數目決定局部寫入，可以顆 hello 資料磁碟的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="3bced-172">hello number of columns determines hello number of parallel writes, which can be striped across hello data disks.</span></span> <span data-ttu-id="3bced-173">因此，任何加入的資料磁碟均無法提升效能。</span><span class="sxs-lookup"><span data-stu-id="3bced-173">Therefore, any added data disks cannot increase performance.</span></span> <span data-ttu-id="3bced-174">它們只可以提供更多存放裝置 hello 正在寫入的資料。</span><span class="sxs-lookup"><span data-stu-id="3bced-174">They can only provide more storage for hello data being written.</span></span> <span data-ttu-id="3bced-175">這項限制也表示，在擴充 hello 磁碟機，資料行的 hello 數目會決定 hello，您可以加入資料磁碟數目下限。</span><span class="sxs-lookup"><span data-stu-id="3bced-175">This limitation also means that, when extending hello drive, hello number of columns determines hello minimum number of data disks that you can add.</span></span> <span data-ttu-id="3bced-176">因此如果您有四個資料磁碟建立存放集區，資料行的 hello 數目也是四個。</span><span class="sxs-lookup"><span data-stu-id="3bced-176">So if you create a storage pool with four data disks, hello number of columns is also four.</span></span> <span data-ttu-id="3bced-177">每當您擴充 hello 存放裝置，您必須新增至少四個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="3bced-177">Any time you extend hello storage, you must add at least four data disks.</span></span>

![延伸 SQL VM 的磁碟機](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a><span data-ttu-id="3bced-179">儲存體組態</span><span class="sxs-lookup"><span data-stu-id="3bced-179">Storage configuration</span></span>
<span data-ttu-id="3bced-180">本節提供的參考 hello SQL VM 佈建或 hello Azure 入口網站中的組態期間自動執行 Azure 儲存體組態變更。</span><span class="sxs-lookup"><span data-stu-id="3bced-180">This section provides a reference for hello storage configuration changes that Azure automatically performs during SQL VM provisioning or configuration in hello Azure Portal.</span></span>

* <span data-ttu-id="3bced-181">如果您為 VM 選取了小於兩個 TB 的儲存體，則 Azure 不會建立存放集區。</span><span class="sxs-lookup"><span data-stu-id="3bced-181">If you have selected fewer than two TBs of storage for your VM, Azure does not create a storage pool.</span></span>
* <span data-ttu-id="3bced-182">如果您為 VM 選取了至少兩個 TB 的儲存體，則 Azure 會設定存放集區。</span><span class="sxs-lookup"><span data-stu-id="3bced-182">If you have selected at least two TBs of storage for your VM, Azure configures a storage pool.</span></span> <span data-ttu-id="3bced-183">本主題的 hello 下一節提供 hello 存放集區設定的 hello 詳細的資料。</span><span class="sxs-lookup"><span data-stu-id="3bced-183">hello next section of this topic provides hello details of hello storage pool configuration.</span></span>
* <span data-ttu-id="3bced-184">自動儲存體設定一律使用 [儲存體](../../../storage/common/storage-premium-storage.md) P30 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="3bced-184">Automatic storage configuration always uses [premium storage](../../../storage/common/storage-premium-storage.md) P30 data disks.</span></span> <span data-ttu-id="3bced-185">因此，沒有 1:1 之間的對應您選取的數字的 Tb，而且資料磁碟數目 hello 附加 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="3bced-185">Consequently, there is a 1:1 mapping between your selected number of Terabytes and hello number of data disks attached tooyour VM.</span></span>

<span data-ttu-id="3bced-186">如需定價資訊，請參閱 hello[儲存體定價](https://azure.microsoft.com/pricing/details/storage)頁面 hello**磁碟儲存體** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3bced-186">For pricing information, see hello [Storage pricing](https://azure.microsoft.com/pricing/details/storage) page on hello **Disk Storage** tab.</span></span>

### <a name="creation-of-hello-storage-pool"></a><span data-ttu-id="3bced-187">建立 hello 存放集區</span><span class="sxs-lookup"><span data-stu-id="3bced-187">Creation of hello storage pool</span></span>
<span data-ttu-id="3bced-188">Azure 會使用下列設定 toocreate hello 存放集區上的 SQL Server Vm 的 hello。</span><span class="sxs-lookup"><span data-stu-id="3bced-188">Azure uses hello following settings toocreate hello storage pool on SQL Server VMs.</span></span>

| <span data-ttu-id="3bced-189">設定</span><span class="sxs-lookup"><span data-stu-id="3bced-189">Setting</span></span> | <span data-ttu-id="3bced-190">值</span><span class="sxs-lookup"><span data-stu-id="3bced-190">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3bced-191">等量大小</span><span class="sxs-lookup"><span data-stu-id="3bced-191">Stripe size</span></span> |<span data-ttu-id="3bced-192">256 KB (資料倉儲)；64 KB (交易式)</span><span class="sxs-lookup"><span data-stu-id="3bced-192">256 KB (Data warehousing); 64 KB (Transactional)</span></span> |
| <span data-ttu-id="3bced-193">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="3bced-193">Disk sizes</span></span> |<span data-ttu-id="3bced-194">每個磁碟 1 TB</span><span class="sxs-lookup"><span data-stu-id="3bced-194">1 TB each</span></span> |
| <span data-ttu-id="3bced-195">快取</span><span class="sxs-lookup"><span data-stu-id="3bced-195">Cache</span></span> |<span data-ttu-id="3bced-196">讀取</span><span class="sxs-lookup"><span data-stu-id="3bced-196">Read</span></span> |
| <span data-ttu-id="3bced-197">配置大小</span><span class="sxs-lookup"><span data-stu-id="3bced-197">Allocation size</span></span> |<span data-ttu-id="3bced-198">64 KB NTFS 配置單位大小</span><span class="sxs-lookup"><span data-stu-id="3bced-198">64 KB NTFS allocation unit size</span></span> |
| <span data-ttu-id="3bced-199">立即檔案初始化</span><span class="sxs-lookup"><span data-stu-id="3bced-199">Instant file initialization</span></span> |<span data-ttu-id="3bced-200">已啟用</span><span class="sxs-lookup"><span data-stu-id="3bced-200">Enabled</span></span> |
| <span data-ttu-id="3bced-201">在記憶體中鎖定頁面</span><span class="sxs-lookup"><span data-stu-id="3bced-201">Lock pages in memory</span></span> |<span data-ttu-id="3bced-202">已啟用</span><span class="sxs-lookup"><span data-stu-id="3bced-202">Enabled</span></span> |
| <span data-ttu-id="3bced-203">復原</span><span class="sxs-lookup"><span data-stu-id="3bced-203">Recovery</span></span> |<span data-ttu-id="3bced-204">簡單復原 (無恢復功能)</span><span class="sxs-lookup"><span data-stu-id="3bced-204">Simple recovery (no resiliency)</span></span> |
| <span data-ttu-id="3bced-205">資料行數目</span><span class="sxs-lookup"><span data-stu-id="3bced-205">Number of columns</span></span> |<span data-ttu-id="3bced-206">資料磁碟數量<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="3bced-206">Number of data disks<sup>1</sup></span></span> |
| <span data-ttu-id="3bced-207">TempDB 位置</span><span class="sxs-lookup"><span data-stu-id="3bced-207">TempDB location</span></span> |<span data-ttu-id="3bced-208">儲存在資料磁碟上<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="3bced-208">Stored on data disks<sup>2</sup></span></span> |

<span data-ttu-id="3bced-209"><sup>1</sup> hello 存放集區建立之後，您無法改變 hello hello 存放集區中的資料行數目。</span><span class="sxs-lookup"><span data-stu-id="3bced-209"><sup>1</sup> After hello storage pool is created, you cannot alter hello number of columns in hello storage pool.</span></span>

<span data-ttu-id="3bced-210"><sup>2</sup>此設定僅適用於您建立使用 hello 儲存體組態功能 toohello 第一個磁碟機。</span><span class="sxs-lookup"><span data-stu-id="3bced-210"><sup>2</sup> This setting only applies toohello first drive you create using hello storage configuration feature.</span></span>

## <a name="workload-optimization-settings"></a><span data-ttu-id="3bced-211">工作負載最佳化設定</span><span class="sxs-lookup"><span data-stu-id="3bced-211">Workload optimization settings</span></span>
<span data-ttu-id="3bced-212">hello 下表描述 hello 三個工作負載類型可用的選項以及其對應的最佳化：</span><span class="sxs-lookup"><span data-stu-id="3bced-212">hello following table describes hello three workload type options available and their corresponding optimizations:</span></span>

| <span data-ttu-id="3bced-213">工作負載類型</span><span class="sxs-lookup"><span data-stu-id="3bced-213">Workload type</span></span> | <span data-ttu-id="3bced-214">說明</span><span class="sxs-lookup"><span data-stu-id="3bced-214">Description</span></span> | <span data-ttu-id="3bced-215">最佳化</span><span class="sxs-lookup"><span data-stu-id="3bced-215">Optimizations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3bced-216">**一般**</span><span class="sxs-lookup"><span data-stu-id="3bced-216">**General**</span></span> |<span data-ttu-id="3bced-217">支援大多數工作負載的預設設定</span><span class="sxs-lookup"><span data-stu-id="3bced-217">Default setting that supports most workloads</span></span> |<span data-ttu-id="3bced-218">None</span><span class="sxs-lookup"><span data-stu-id="3bced-218">None</span></span> |
| <span data-ttu-id="3bced-219">**交易式處理**</span><span class="sxs-lookup"><span data-stu-id="3bced-219">**Transactional processing**</span></span> |<span data-ttu-id="3bced-220">Hello 儲存體的傳統資料庫 OLTP 工作負載最佳化</span><span class="sxs-lookup"><span data-stu-id="3bced-220">Optimizes hello storage for traditional database OLTP workloads</span></span> |<span data-ttu-id="3bced-221">追蹤旗標 1117</span><span class="sxs-lookup"><span data-stu-id="3bced-221">Trace Flag 1117</span></span><br/><span data-ttu-id="3bced-222">追蹤旗標 1118</span><span class="sxs-lookup"><span data-stu-id="3bced-222">Trace Flag 1118</span></span> |
| <span data-ttu-id="3bced-223">**資料倉儲**</span><span class="sxs-lookup"><span data-stu-id="3bced-223">**Data warehousing**</span></span> |<span data-ttu-id="3bced-224">Hello 儲存體分析和報告工作負載最佳化</span><span class="sxs-lookup"><span data-stu-id="3bced-224">Optimizes hello storage for analytic and reporting workloads</span></span> |<span data-ttu-id="3bced-225">追蹤旗標 610</span><span class="sxs-lookup"><span data-stu-id="3bced-225">Trace Flag 610</span></span><br/><span data-ttu-id="3bced-226">追蹤旗標 1117</span><span class="sxs-lookup"><span data-stu-id="3bced-226">Trace Flag 1117</span></span> |

> [!NOTE]
> <span data-ttu-id="3bced-227">您可以在 hello 儲存體組態步驟中選取佈建 SQL 虛擬機器時，您可以只指定 hello 工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="3bced-227">You can only specify hello workload type when you provision a SQL virtual machine by selecting it in hello storage configuration step.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3bced-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bced-228">Next steps</span></span>
<span data-ttu-id="3bced-229">如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3bced-229">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
