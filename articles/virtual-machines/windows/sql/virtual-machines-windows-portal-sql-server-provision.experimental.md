---
title: "SQL Server 虛擬機器 aaaProvision |Microsoft 文件"
description: "建立並使用 hello 入口網站在 Azure 中的 tooa SQL Server 虛擬機器連線。 本教學課程使用 hello Resource Manager 模式。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a><span data-ttu-id="04628-104">佈建 hello Azure 入口網站中的 SQL Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="04628-104">Provision a SQL Server virtual machine in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04628-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="04628-105">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="04628-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="04628-106">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="04628-107">此端對端教學課程會示範如何 toouse 會 hello Azure 入口網站 tooprovision 執行 SQL Server 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04628-107">This end-to-end tutorial shows you how toouse hello Azure Portal tooprovision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="04628-108">hello Azure 虛擬機器 (VM) 映像庫含有包含 Microsoft SQL Server 的數個映像。</span><span class="sxs-lookup"><span data-stu-id="04628-108">hello Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="04628-109">按幾下，您可以選取其中一個 hello SQL VM 映像從 hello 組件庫，並佈建 Azure 環境中。</span><span class="sxs-lookup"><span data-stu-id="04628-109">With a few clicks, you can select one of hello SQL VM images from hello gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="04628-110">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="04628-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="04628-111">從 hello 庫中選取的 SQL VM 映像</span><span class="sxs-lookup"><span data-stu-id="04628-111">Select a SQL VM image from hello gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="04628-112">設定並建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="04628-112">Configure and create hello VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="04628-113">使用遠端桌面開啟 hello VM</span><span class="sxs-lookup"><span data-stu-id="04628-113">Open hello VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="04628-114">從遠端連線 tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="04628-114">Connect tooSQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a><span data-ttu-id="04628-115">從 hello 庫中選取的 SQL VM 映像</span><span class="sxs-lookup"><span data-stu-id="04628-115">Select a SQL VM image from hello gallery</span></span>
1. <span data-ttu-id="04628-116">登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="04628-116">Log in toohello [Azure portal](https://portal.azure.com) using your account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="04628-117">如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="04628-117">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

2. <span data-ttu-id="04628-118">在 hello Azure 入口網站，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="04628-118">On hello Azure portal, click **New**.</span></span> <span data-ttu-id="04628-119">hello 入口網站開啟 hello**新增**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="04628-119">hello portal opens hello **New** blade.</span></span> <span data-ttu-id="04628-120">hello SQL Server VM 資源位於 hello**計算**hello Marketplace 的群組。</span><span class="sxs-lookup"><span data-stu-id="04628-120">hello SQL Server VM resources are in hello **Compute** group of hello Marketplace.</span></span>
3. <span data-ttu-id="04628-121">在 hello**新增**刀鋒視窗中，按一下 **計算**，然後按一下**查看所有**。</span><span class="sxs-lookup"><span data-stu-id="04628-121">In hello **New** blade, click **Compute** and then click **See all**.</span></span>
4. <span data-ttu-id="04628-122">在 hello**篩選**文字方塊中，輸入 SQL Server，然後按下 hello ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="04628-122">In hello **Filter** text box type SQL Server, and press hello ENTER key.</span></span>

   ![Azure 虛擬機器刀鋒視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="04628-124">檢閱 hello 可用的 SQL Server 映像。</span><span class="sxs-lookup"><span data-stu-id="04628-124">Review hello available SQL Server images.</span></span> <span data-ttu-id="04628-125">每個映像皆識別一個 SQL Server 版本和一個作業系統。</span><span class="sxs-lookup"><span data-stu-id="04628-125">Each image identifies a SQL Server version and an operating system.</span></span> 
6. <span data-ttu-id="04628-126">選取 SQL Server 2016 SP1 開發人員在 Windows Server 2016 上 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="04628-126">Select hello image for SQL Server 2016 SP1 Developer on Windows Server 2016.</span></span>

   > [!TIP]
   > <span data-ttu-id="04628-127">hello Developer edition 會使用在本教學課程中，因為它是免費提供給開發測試用途的 SQL server 完整版本。</span><span class="sxs-lookup"><span data-stu-id="04628-127">hello Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes.</span></span> <span data-ttu-id="04628-128">您需支付只執行 hello VM hello 成本。</span><span class="sxs-lookup"><span data-stu-id="04628-128">You pay only for hello cost of running hello VM.</span></span>

   > [!NOTE]
   > <span data-ttu-id="04628-129">SQL VM 映像併入 hello 授權成本 for SQL Server hello 每分鐘定價的 hello （除了 hello developer Edition 和 Express edition) 您建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="04628-129">SQL VM images include hello licensing costs for SQL Server into hello per-minute pricing of hello VM you create (except for hello Developer and Express editions).</span></span> <span data-ttu-id="04628-130">SQL Server Developer 免費供開發/測試 (非生產環境) 使用，SQL Express 免費供輕量型工作負載 (少於 1GB 記憶體、小於 10 GB 儲存體) 使用。</span><span class="sxs-lookup"><span data-stu-id="04628-130">SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1 GB memory, less than 10-GB storage).</span></span>
   > <span data-ttu-id="04628-131">還有另一個選項 toobring 您-擁有的授權 (BYOL) 和 hello VM 工資。</span><span class="sxs-lookup"><span data-stu-id="04628-131">There is another option toobring-your-own-license (BYOL) and pay only for hello VM.</span></span> <span data-ttu-id="04628-132">這些映像的名稱前面會有 {BYOL}。</span><span class="sxs-lookup"><span data-stu-id="04628-132">Those image names are prefixed with {BYOL}.</span></span> <span data-ttu-id="04628-133">如需這些選項的詳細資訊，請參閱 [SQL Server Azure VM 的定價指導方針](virtual-machines-windows-sql-server-pricing-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-133">For more information on these options, see [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

7. <span data-ttu-id="04628-134">在 [選取部署模型] 底下，確認已選取 [Resource Manager]。</span><span class="sxs-lookup"><span data-stu-id="04628-134">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="04628-135">資源管理員是 hello 建議新的虛擬機器的部署模型。</span><span class="sxs-lookup"><span data-stu-id="04628-135">Resource Manager is hello recommended deployment model for new virtual machines.</span></span> <span data-ttu-id="04628-136">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="04628-136">Click **Create**.</span></span>

    ![使用 Resource Manager 建立 SQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a><span data-ttu-id="04628-138">設定 hello VM</span><span class="sxs-lookup"><span data-stu-id="04628-138">Configure hello VM</span></span>
<span data-ttu-id="04628-139">有五個刀鋒視窗可用來設定 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04628-139">There are five blades for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="04628-140">步驟</span><span class="sxs-lookup"><span data-stu-id="04628-140">Step</span></span> | <span data-ttu-id="04628-141">說明</span><span class="sxs-lookup"><span data-stu-id="04628-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04628-142">**基本概念**</span><span class="sxs-lookup"><span data-stu-id="04628-142">**Basics**</span></span> |[<span data-ttu-id="04628-143">設定基本設定</span><span class="sxs-lookup"><span data-stu-id="04628-143">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="04628-144">**大小**</span><span class="sxs-lookup"><span data-stu-id="04628-144">**Size**</span></span> |[<span data-ttu-id="04628-145">選擇虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="04628-145">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="04628-146">**設定**</span><span class="sxs-lookup"><span data-stu-id="04628-146">**Settings**</span></span> |[<span data-ttu-id="04628-147">設定選用功能</span><span class="sxs-lookup"><span data-stu-id="04628-147">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="04628-148">**SQL Server 設定**</span><span class="sxs-lookup"><span data-stu-id="04628-148">**SQL Server settings**</span></span> |[<span data-ttu-id="04628-149">進行 SQL Server 設定</span><span class="sxs-lookup"><span data-stu-id="04628-149">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="04628-150">**摘要**</span><span class="sxs-lookup"><span data-stu-id="04628-150">**Summary**</span></span> |[<span data-ttu-id="04628-151">檢閱 hello 摘要</span><span class="sxs-lookup"><span data-stu-id="04628-151">Review hello summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="04628-152">1.設定基本設定</span><span class="sxs-lookup"><span data-stu-id="04628-152">1. Configure basic settings</span></span>
<span data-ttu-id="04628-153">在 hello**基本概念**刀鋒視窗中，提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="04628-153">On hello **Basics** blade, provide hello following information:</span></span>

* <span data-ttu-id="04628-154">輸入唯一的虛擬機器 [名稱] 。</span><span class="sxs-lookup"><span data-stu-id="04628-154">Enter a unique virtual machine **Name**.</span></span>
* <span data-ttu-id="04628-155">指定**使用者名**hello hello VM 上的本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="04628-155">Specify a **User name** for hello local administrator account on hello VM.</span></span> <span data-ttu-id="04628-156">此帳戶也會加入 SQL Server toohello **sysadmin**固定的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="04628-156">This account is also added toohello SQL Server **sysadmin** fixed server role.</span></span>
* <span data-ttu-id="04628-157">提供強式 [密碼] 。</span><span class="sxs-lookup"><span data-stu-id="04628-157">Provide a strong **Password**.</span></span>
* <span data-ttu-id="04628-158">如果您有多個訂閱，請確認 hello 訂用帳戶的正確 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="04628-158">If you have multiple subscriptions, verify that hello subscription is correct for hello new VM.</span></span>
* <span data-ttu-id="04628-159">在 hello**資源群組**方塊中，輸入新的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="04628-159">In hello **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="04628-160">或者，toouse 現有的資源群組按一下**使用現有**。</span><span class="sxs-lookup"><span data-stu-id="04628-160">Alternatively, toouse an existing resource group click **Use existing**.</span></span> <span data-ttu-id="04628-161">資源群組是 Azure (虛擬機器、儲存體帳戶、虛擬網路等) 中相關資源的集合。</span><span class="sxs-lookup"><span data-stu-id="04628-161">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="04628-162">如果您只是測試或了解 Azure 中的 SQL Server 部署，使用新的資源群組很有幫助。</span><span class="sxs-lookup"><span data-stu-id="04628-162">Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure.</span></span> <span data-ttu-id="04628-163">完成測試之後，刪除 hello 資源群組 tooautomatically 刪除 hello VM 和資源群組相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="04628-163">After you finish with your test, delete hello resource group tooautomatically delete hello VM and all resources associated with that resource group.</span></span> <span data-ttu-id="04628-164">如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-164">For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).</span></span>
  > 
  > 
* <span data-ttu-id="04628-165">選取此部署的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="04628-165">Select a **Location** for this deployment.</span></span>
* <span data-ttu-id="04628-166">按一下**確定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="04628-166">Click **OK** toosave hello settings.</span></span>
  
    ![SQL 基本概念刀鋒視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="04628-168">2.選擇虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="04628-168">2. Choose virtual machine size</span></span>
<span data-ttu-id="04628-169">在 hello**大小**步驟中，虛擬機器大小選擇 「 hello 中**大小選擇 「**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="04628-169">On hello **Size** step, choose a virtual machine size in hello **Choose a size** blade.</span></span> <span data-ttu-id="04628-170">hello 刀鋒視窗一開始會顯示您所選取的 hello 映像為基礎的建議的機器大小。</span><span class="sxs-lookup"><span data-stu-id="04628-170">hello blade initially displays recommended machine sizes based on hello image you selected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04628-171">hello 估計 hello 上顯示的每月成本**大小選擇 「**刀鋒視窗中不包含 SQL Server 授權成本。</span><span class="sxs-lookup"><span data-stu-id="04628-171">hello estimated monthly cost displayed on hello **Choose a size** blade does not include SQL Server licensing costs.</span></span> <span data-ttu-id="04628-172">此預估每月成本是單獨的 VM hello hello 成本。</span><span class="sxs-lookup"><span data-stu-id="04628-172">This estimated monthly cost is hello cost of hello VM alone.</span></span> <span data-ttu-id="04628-173">Hello Express 和 Developer edition 的 SQL Server，這是 hello 總估計的成本。</span><span class="sxs-lookup"><span data-stu-id="04628-173">For hello Express and Developer editions of SQL Server, this is hello total estimated cost.</span></span> <span data-ttu-id="04628-174">對於其他版本，請參閱 hello [Windows 虛擬機器定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)並選取您目標的 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="04628-174">For other editions, see hello [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server.</span></span> <span data-ttu-id="04628-175">另請參閱 hello[定價指導方針 SQL Server 的 Azure Vm](virtual-machines-windows-sql-server-pricing-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-175">Also see hello [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

![SQL VM 大小選項](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="04628-177">針對生產工作負載，建議選取可支援 [進階儲存體](../../../storage/storage-premium-storage.md)的虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="04628-177">For production workloads, we recommend selecting a virtual machine size that supports [Premium Storage](../../../storage/storage-premium-storage.md).</span></span> <span data-ttu-id="04628-178">如果您不需要該層級的效能，使用 hello**檢視所有**按鈕，顯示所有機器的大小選項。</span><span class="sxs-lookup"><span data-stu-id="04628-178">If you do not require that level of performance, use hello **View all** button, which shows all machine size options.</span></span> <span data-ttu-id="04628-179">例如，您可能會將較小的機器使用開發或測試環境。</span><span class="sxs-lookup"><span data-stu-id="04628-179">For example, you might use a smaller machine size for a development or test environment.</span></span>

> [!NOTE]
> <span data-ttu-id="04628-180">如需關於虛擬機器大小的詳細資訊，請參閱[虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="04628-180">For more information about virtual machine sizes, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="04628-181">如需有關 SQL Server VM 大小的考量，請參閱 [Azure 虛擬機器中的 SQL Server 效能最佳作法](virtual-machines-windows-sql-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-181">For considerations about SQL Server VM sizes, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

<span data-ttu-id="04628-182">選擇您的機器大小，然後按一下選取 。</span><span class="sxs-lookup"><span data-stu-id="04628-182">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="04628-183">3.設定選用功能</span><span class="sxs-lookup"><span data-stu-id="04628-183">3. Configure optional features</span></span>
<span data-ttu-id="04628-184">在 hello**設定**刀鋒視窗中，設定 Azure 儲存體、 網路功能與監視 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04628-184">On hello **Settings** blade, configure Azure storage, networking, and monitoring for hello virtual machine.</span></span>

* <span data-ttu-id="04628-185">在 [儲存體] 底下，指定 [標準] 或 [進階 (SSD)] 的 [磁碟類型]。</span><span class="sxs-lookup"><span data-stu-id="04628-185">Under **Storage**, specify a **Disk type** of either Standard or Premium (SSD).</span></span> <span data-ttu-id="04628-186">針對生產環境工作負載，建議使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="04628-186">Premium storage is recommended for production workloads.</span></span>

> [!NOTE]
> <span data-ttu-id="04628-187">如果您對不支援進階儲存體的機器大小選取 [進階 (SSD)]，您的機器大小會自動變更。</span><span class="sxs-lookup"><span data-stu-id="04628-187">If you select Premium (SSD) for a machine size that does not support Premium Storage, your machine size changes automatically.</span></span>  
> 
> 

* <span data-ttu-id="04628-188">在下**儲存體帳戶**，您可以接受 hello 自動佈建儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="04628-188">Under **Storage account**, you can accept hello automatically provisioned storage account name.</span></span> <span data-ttu-id="04628-189">您也可以按一下**儲存體帳戶**toochoose 現有帳戶並設定 hello 儲存體帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="04628-189">You can also click on **Storage account** toochoose an existing account and configure hello storage account type.</span></span> <span data-ttu-id="04628-190">Azure 預設會建立具有本地備援儲存體的新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="04628-190">By default, Azure creates a new storage account with locally redundant storage.</span></span> <span data-ttu-id="04628-191">如需儲存體選項的詳細資訊，請參閱 [Azure 儲存體複寫](../../../storage/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-191">For more information about storage options, see [Azure Storage replication](../../../storage/storage-redundancy.md).</span></span>
* <span data-ttu-id="04628-192">在下**網路**，您可以接受 hello 自動填入值。</span><span class="sxs-lookup"><span data-stu-id="04628-192">Under **Network**, you can accept hello automatically populated values.</span></span> <span data-ttu-id="04628-193">您也可以按一下每個功能 toomanually 設定 hello**虛擬網路**，**子網路**，**公用 IP 位址**，和**網路安全性群組**.</span><span class="sxs-lookup"><span data-stu-id="04628-193">You can also click on each feature toomanually configure hello **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="04628-194">基於 hello 本教學課程中，保留 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="04628-194">For hello purposes of this tutorial, keep hello default values.</span></span>
* <span data-ttu-id="04628-195">Azure 可讓**監視**預設與 hello hello VM 為指定的相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="04628-195">Azure enables **Monitoring** by default with hello same storage account designated for hello VM.</span></span> <span data-ttu-id="04628-196">您可以在這裡變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="04628-196">You can change these settings here.</span></span>
* <span data-ttu-id="04628-197">在 [可用性設定組] 底下，指定可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="04628-197">Under **Availability set**, specify an availability set.</span></span> <span data-ttu-id="04628-198">基於 hello 本教學課程，您可以選取**無**。</span><span class="sxs-lookup"><span data-stu-id="04628-198">For hello purposes of this tutorial, you can select **none**.</span></span> <span data-ttu-id="04628-199">如果您計劃 tooset SQL AlwaysOn 可用性群組上的，設定 hello 可用性 tooavoid 重建 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04628-199">If you plan tooset up SQL AlwaysOn Availability Groups, configure hello availability tooavoid recreating hello virtual machine.</span></span>  <span data-ttu-id="04628-200">如需詳細資訊，請參閱[管理 hello 虛擬機器可用性](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="04628-200">For more information, see [Manage hello Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="04628-201">完成這些設定時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="04628-201">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="04628-202">4.進行 SQL Server 設定</span><span class="sxs-lookup"><span data-stu-id="04628-202">4. Configure SQL server settings</span></span>
<span data-ttu-id="04628-203">在 hello **SQL Server 設定**刀鋒視窗中，設定特定的設定和針對 SQL Server 最佳化。</span><span class="sxs-lookup"><span data-stu-id="04628-203">On hello **SQL Server settings** blade, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="04628-204">您可以設定 SQL Server 的 hello 設定包括下列設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="04628-204">hello settings that you can configure for SQL Server include hello following settings.</span></span>

| <span data-ttu-id="04628-205">設定</span><span class="sxs-lookup"><span data-stu-id="04628-205">Setting</span></span> |
| --- |
| [<span data-ttu-id="04628-206">連線能力</span><span class="sxs-lookup"><span data-stu-id="04628-206">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="04628-207">驗證</span><span class="sxs-lookup"><span data-stu-id="04628-207">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="04628-208">儲存體組態</span><span class="sxs-lookup"><span data-stu-id="04628-208">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="04628-209">自動修補</span><span class="sxs-lookup"><span data-stu-id="04628-209">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="04628-210">自動備份</span><span class="sxs-lookup"><span data-stu-id="04628-210">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="04628-211">Azure 金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="04628-211">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="04628-212">R 服務</span><span class="sxs-lookup"><span data-stu-id="04628-212">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="04628-213">連線能力</span><span class="sxs-lookup"><span data-stu-id="04628-213">Connectivity</span></span>
<span data-ttu-id="04628-214">在下**SQL 連接性**，指定 hello 類型要 toohello 這部 vm 的 SQL Server 執行個體的存取。</span><span class="sxs-lookup"><span data-stu-id="04628-214">Under **SQL connectivity**, specify hello type of access you want toohello SQL Server instance on this VM.</span></span> <span data-ttu-id="04628-215">基於 hello 本教學課程中，選取**公用 （網際網路）**從機器或服務上的 tooallow 連線 tooSQL 伺服器 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="04628-215">For hello purposes of this tutorial, select **Public (internet)** tooallow connections tooSQL Server from machines or services on hello internet.</span></span> <span data-ttu-id="04628-216">選取此選項，Azure 會自動設定 hello 防火牆與 hello 網路安全性的群組 tooallow 流量通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="04628-216">With this option selected, Azure automatically configures hello firewall and hello network security group tooallow traffic on port 1433.</span></span>  

![SQL 連線選項](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

<span data-ttu-id="04628-218">tooconnect tooSQL 伺服器 hello 透過網際網路，您也必須啟用 SQL Server 驗證，hello 下一節中所述。</span><span class="sxs-lookup"><span data-stu-id="04628-218">tooconnect tooSQL Server via hello internet, you also must enable SQL Server Authentication, which is described in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="04628-219">它是可能 tooadd hello 網路通訊 tooyour SQL Server VM 的更多限制。</span><span class="sxs-lookup"><span data-stu-id="04628-219">It is possible tooadd more restrictions for hello network communications tooyour SQL Server VM.</span></span> <span data-ttu-id="04628-220">建立 hello VM 之後，您可以加入更多的限制所編輯的 hello 網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="04628-220">You can add more restrictions by editing hello Network Security Group after hello VM is created.</span></span> <span data-ttu-id="04628-221">如需詳細資訊，請參閱 [什麼是網路安全性群組 (NSG)？](../../../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="04628-221">For more information, see [What is a Network Security Group (NSG)?](../../../virtual-network/virtual-networks-nsg.md)</span></span>
> 
> 

<span data-ttu-id="04628-222">如果您希望 Database Engine toonot 啟用連線 toohello 透過 hello 網際網路，選擇其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="04628-222">If you would prefer toonot enable connections toohello Database Engine via hello internet, choose one of hello following options:</span></span>

* <span data-ttu-id="04628-223">**（在 VM 只) 內本機**tooallow 連線 tooSQL 只能從伺服器 hello VM 內。</span><span class="sxs-lookup"><span data-stu-id="04628-223">**Local (inside VM only)** tooallow connections tooSQL Server only from within hello VM.</span></span>
* <span data-ttu-id="04628-224">**（在虛擬網路） 內的私用**從機器或服務在 hello tooallow 連線 tooSQL 伺服器相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="04628-224">**Private (within Virtual Network)** tooallow connections tooSQL Server from machines or services in hello same virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="04628-225">適用於 SQL Server Express edition 的 hello 虛擬機器映像不會自動啟用 hello TCP/IP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="04628-225">hello virtual machine image for SQL Server Express edition does not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="04628-226">這是即使的 hello 公用與私人連線，則為 true 的選項。</span><span class="sxs-lookup"><span data-stu-id="04628-226">This is true even for hello Public and  Private connectivity options.</span></span> <span data-ttu-id="04628-227">Express 版本中，您必須用於 SQL Server 組態管理員太[手動啟用 hello TCP/IP 通訊協定](#configure-sql-server-to-listen-on-the-tcp-protocol)之後建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="04628-227">For Express edition, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating hello VM.</span></span>
> 
> 

<span data-ttu-id="04628-228">一般情況下，選擇 hello 限制最嚴格連線能力，可讓您的案例來改善安全性。</span><span class="sxs-lookup"><span data-stu-id="04628-228">In general, improve security by choosing hello most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="04628-229">但所有 hello 選項都會透過網路安全性群組規則和 SQL/Windows 驗證安全性實體。</span><span class="sxs-lookup"><span data-stu-id="04628-229">But all hello options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span>

<span data-ttu-id="04628-230">**連接埠**too1433 預設值。</span><span class="sxs-lookup"><span data-stu-id="04628-230">**Port** defaults too1433.</span></span> <span data-ttu-id="04628-231">您可以指定其他連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="04628-231">You can specify a different port number.</span></span>
<span data-ttu-id="04628-232">如需詳細資訊，請參閱[連接 tooa SQL Server 虛擬機器 （資源管理員） |Microsoft Azure](virtual-machines-windows-sql-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-232">For more information, see [Connect tooa SQL Server Virtual Machine (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md).</span></span>

### <a name="authentication"></a><span data-ttu-id="04628-233">驗證</span><span class="sxs-lookup"><span data-stu-id="04628-233">Authentication</span></span>
<span data-ttu-id="04628-234">如果您需要「SQL Server 驗證」，請按一下 [SQL 驗證]  under 。</span><span class="sxs-lookup"><span data-stu-id="04628-234">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![SQL Server 驗證](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> <span data-ttu-id="04628-236">如果您打算 tooaccess SQL Server 透過 hello 網際網路 (也就是 hello 公用連線選項)，您必須啟用 SQL 驗證這裡。</span><span class="sxs-lookup"><span data-stu-id="04628-236">If you plan tooaccess SQL Server over hello internet (that is, hello Public connectivity option), you must enable SQL authentication here.</span></span> <span data-ttu-id="04628-237">SQL Server 的公用存取 toohello 需要 hello 使用 SQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="04628-237">Public access toohello SQL Server requires hello use of SQL Authentication.</span></span>
> 
> 

<span data-ttu-id="04628-238">如果您啟用 [SQL Server 驗證]，請指定 [登入名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="04628-238">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="04628-239">這個使用者名稱設定為 SQL Server 驗證登入和成員的 hello **sysadmin**固定的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="04628-239">This user name is configured as a SQL Server Authentication login and member of hello **sysadmin** fixed server role.</span></span> <span data-ttu-id="04628-240">如需驗證模式的詳細資訊，請參閱[選擇驗證模式](http://msdn.microsoft.com/library/ms144284.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04628-240">For more information about Authentication Modes, see [Choose an Authentication Mode](http://msdn.microsoft.com/library/ms144284.aspx).</span></span>

<span data-ttu-id="04628-241">如果您未啟用 SQL Server 驗證，然後您就可以使用本機系統管理員帳戶 hello hello VM tooconnect toohello SQL Server 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="04628-241">If you do not enable SQL Server Authentication, then you can use hello local Administrator account on hello VM tooconnect toohello SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="04628-242">儲存體組態</span><span class="sxs-lookup"><span data-stu-id="04628-242">Storage configuration</span></span>
<span data-ttu-id="04628-243">按一下**儲存體設定**toospecify hello 存放裝置需求。</span><span class="sxs-lookup"><span data-stu-id="04628-243">Click **Storage configuration** toospecify hello storage requirements.</span></span>

![SQL 儲存體組態](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> <span data-ttu-id="04628-245">如果您選取 [標準] 儲存體，則無法使用此選項。</span><span class="sxs-lookup"><span data-stu-id="04628-245">If you select Standard storage, this option is not available.</span></span> <span data-ttu-id="04628-246">自動儲存體最佳化只適用於進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="04628-246">Automatic storage optimization is available only for Premium Storage.</span></span>
> 
> 

<span data-ttu-id="04628-247">您可以用每秒輸入/輸出作業數 (IOPs)、輸送量 (單位為 MB/s) 及總儲存體大小來指定需求。</span><span class="sxs-lookup"><span data-stu-id="04628-247">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="04628-248">使用 hello 滑動縮放比例，以設定這些值。</span><span class="sxs-lookup"><span data-stu-id="04628-248">Configure these values by using hello sliding scales.</span></span> <span data-ttu-id="04628-249">hello 入口網站會自動計算 hello 根據這些需求的磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="04628-249">hello portal automatically calculates hello number of disks based on these requirements.</span></span>

<span data-ttu-id="04628-250">根據預設，Azure hello 儲存體最佳化 5000 IOPs、 200 Mb，和 1 TB 的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="04628-250">By default, Azure optimizes hello storage for 5000 IOPs, 200 MBs, and 1 TB of storage space.</span></span> <span data-ttu-id="04628-251">您可以根據工作負載變更這些儲存體設定。</span><span class="sxs-lookup"><span data-stu-id="04628-251">You can change these storage settings based on workload.</span></span> <span data-ttu-id="04628-252">在下**針對儲存體最佳化**，選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="04628-252">Under **Storage optimized for**, select one of hello following options:</span></span>

* <span data-ttu-id="04628-253">**一般**hello 預設設定，並且支援大部分的工作負載。</span><span class="sxs-lookup"><span data-stu-id="04628-253">**General** is hello default setting and supports most workloads.</span></span>
* <span data-ttu-id="04628-254">**交易式**傳統資料庫 OLTP 工作負載的 hello 儲存體的處理最佳化。</span><span class="sxs-lookup"><span data-stu-id="04628-254">**Transactional** processing optimizes hello storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="04628-255">**資料倉儲**hello 儲存體分析和報告工作負載最佳化。</span><span class="sxs-lookup"><span data-stu-id="04628-255">**Data warehousing** optimizes hello storage for analytic and reporting workloads.</span></span>

> [!NOTE]
> <span data-ttu-id="04628-256">hello hello 滑桿上方限制是根據您選取的虛擬機器的大小而有所不同。</span><span class="sxs-lookup"><span data-stu-id="04628-256">hello upper limits on hello sliders vary depending on your selected virtual machine size.</span></span>
> 
> 

### <a name="automated-patching"></a><span data-ttu-id="04628-257">自動修補</span><span class="sxs-lookup"><span data-stu-id="04628-257">Automated patching</span></span>
<span data-ttu-id="04628-258">**Automated patching** 。</span><span class="sxs-lookup"><span data-stu-id="04628-258">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="04628-259">自動修補允許 Azure tooautomatically 修補 SQL Server 和 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="04628-259">Automated patching allows Azure tooautomatically patch SQL Server and hello operating system.</span></span> <span data-ttu-id="04628-260">指定一天的 hello 週、 時間和維護期間的持續時間。</span><span class="sxs-lookup"><span data-stu-id="04628-260">Specify a day of hello week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="04628-261">Azure 會在此維護期間執行修補。</span><span class="sxs-lookup"><span data-stu-id="04628-261">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="04628-262">hello 維護窗口排程會為時間使用 hello VM 地區設定。</span><span class="sxs-lookup"><span data-stu-id="04628-262">hello maintenance window schedule uses hello VM locale for time.</span></span> <span data-ttu-id="04628-263">如果不想使用 Azure tooautomatically 修補 SQL Server 和 hello 作業系統，請按一下**停用**。</span><span class="sxs-lookup"><span data-stu-id="04628-263">If you do not want Azure tooautomatically patch SQL Server and hello operating system, click **Disable**.</span></span>  

![SQL 自動修補](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="04628-265">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補](virtual-machines-windows-sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-265">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="04628-266">自動備份</span><span class="sxs-lookup"><span data-stu-id="04628-266">Automated backup</span></span>
<span data-ttu-id="04628-267">在 [自動備份] 底下，可以為所有資料庫啟用自動資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="04628-267">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="04628-268">預設會停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="04628-268">Automated backup is disabled by default.</span></span>

<span data-ttu-id="04628-269">當您啟用 SQL 自動的備份時，您可以設定下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="04628-269">When you enable SQL automated backup, you can configure hello following settings:</span></span>

* <span data-ttu-id="04628-270">備份的保留期限 (天數)</span><span class="sxs-lookup"><span data-stu-id="04628-270">Retention period (days) for backups</span></span>
* <span data-ttu-id="04628-271">備份的儲存體帳戶 toouse</span><span class="sxs-lookup"><span data-stu-id="04628-271">Storage account toouse for backups</span></span>
* <span data-ttu-id="04628-272">備份的加密選項和密碼</span><span class="sxs-lookup"><span data-stu-id="04628-272">Encryption option and password for backups</span></span>
* <span data-ttu-id="04628-273">備份系統資料庫</span><span class="sxs-lookup"><span data-stu-id="04628-273">Backup system databases</span></span>
* <span data-ttu-id="04628-274">設定備份排程</span><span class="sxs-lookup"><span data-stu-id="04628-274">Configure backup schedule</span></span>

<span data-ttu-id="04628-275">tooencrypt hello 備份、 按一下**啟用**。</span><span class="sxs-lookup"><span data-stu-id="04628-275">tooencrypt hello backup, click **Enable**.</span></span> <span data-ttu-id="04628-276">然後指定 hello**密碼**。</span><span class="sxs-lookup"><span data-stu-id="04628-276">Then specify hello **Password**.</span></span> <span data-ttu-id="04628-277">Azure 會建立憑證 tooencrypt hello 備份，並使用 hello 指定密碼 tooprotect 該憑證。</span><span class="sxs-lookup"><span data-stu-id="04628-277">Azure creates a certificate tooencrypt hello backups and uses hello specified password tooprotect that certificate.</span></span>

![SQL 自動備份](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="04628-279">如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的自動化備份](virtual-machines-windows-sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-279">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="04628-280">Azure 金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="04628-280">Azure Key Vault integration</span></span>
<span data-ttu-id="04628-281">按一下 toostore 安全性密碼，在 Azure 中的進行加密， **Azure 金鑰保存庫整合**按一下**啟用**。</span><span class="sxs-lookup"><span data-stu-id="04628-281">toostore security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure 金鑰保存庫整合](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="04628-283">hello 下表列出 hello 參數需要的 tooconfigure Azure 金鑰保存庫整合。</span><span class="sxs-lookup"><span data-stu-id="04628-283">hello following table lists hello parameters required tooconfigure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="04628-284">參數</span><span class="sxs-lookup"><span data-stu-id="04628-284">PARAMETER</span></span> | <span data-ttu-id="04628-285">說明</span><span class="sxs-lookup"><span data-stu-id="04628-285">DESCRIPTION</span></span> | <span data-ttu-id="04628-286">範例</span><span class="sxs-lookup"><span data-stu-id="04628-286">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04628-287">**金鑰保存庫 URL**</span><span class="sxs-lookup"><span data-stu-id="04628-287">**Key Vault URL**</span></span> |<span data-ttu-id="04628-288">hello hello 金鑰保存庫位置。</span><span class="sxs-lookup"><span data-stu-id="04628-288">hello location of hello key vault.</span></span> |<span data-ttu-id="04628-289">https://contosokeyvault.vault.azure.net/</span><span class="sxs-lookup"><span data-stu-id="04628-289">https://contosokeyvault.vault.azure.net/</span></span> |
| <span data-ttu-id="04628-290">**主體名稱**</span><span class="sxs-lookup"><span data-stu-id="04628-290">**Principal name**</span></span> |<span data-ttu-id="04628-291">Azure Active Directory 服務主體名稱。</span><span class="sxs-lookup"><span data-stu-id="04628-291">Azure Active Directory service principal name.</span></span> <span data-ttu-id="04628-292">此名稱也是參考的 tooas hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="04628-292">This name is also referred tooas hello Client ID.</span></span> |<span data-ttu-id="04628-293">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="04628-293">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="04628-294">**主體密碼**</span><span class="sxs-lookup"><span data-stu-id="04628-294">**Principal secret**</span></span> |<span data-ttu-id="04628-295">Azure Active Directory 服務主體密碼。</span><span class="sxs-lookup"><span data-stu-id="04628-295">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="04628-296">這個密碼也會參照的 tooas hello 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="04628-296">This secret is also referred tooas hello Client Secret.</span></span> |<span data-ttu-id="04628-297">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="04628-297">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="04628-298">**認證名稱**</span><span class="sxs-lookup"><span data-stu-id="04628-298">**Credential name**</span></span> |<span data-ttu-id="04628-299">**認證名稱**: AKV 整合建立 SQL Server，讓 hello VM toohave 存取 toohello 金鑰保存庫中的認證。</span><span class="sxs-lookup"><span data-stu-id="04628-299">**Credential name**: AKV Integration creates a credential within SQL Server, allowing hello VM toohave access toohello key vault.</span></span> <span data-ttu-id="04628-300">選擇此認證的名稱。</span><span class="sxs-lookup"><span data-stu-id="04628-300">Choose a name for this credential.</span></span> |<span data-ttu-id="04628-301">mycred1</span><span class="sxs-lookup"><span data-stu-id="04628-301">mycred1</span></span> |

<span data-ttu-id="04628-302">如需詳細資訊，請參閱 [在 Azure VM 上設定 SQL Server 的 Azure 金鑰保存庫整合](virtual-machines-windows-ps-sql-keyvault.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-302">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

<span data-ttu-id="04628-303">完成 SQL Server 設定之後，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="04628-303">When you are finished configuring SQL Server settings, click **OK**.</span></span>

### <a name="r-services"></a><span data-ttu-id="04628-304">R 服務</span><span class="sxs-lookup"><span data-stu-id="04628-304">R services</span></span>
<span data-ttu-id="04628-305">您可以啟用 [SQL Server R 服務](https://msdn.microsoft.com/library/mt604845.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04628-305">You can enable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="04628-306">SQL Server R Services 可讓您使用 SQL Server 2016 toouse 進階分析。</span><span class="sxs-lookup"><span data-stu-id="04628-306">SQL Server R Services enables you toouse advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="04628-307">按一下**啟用**上 hello **SQL Server 設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="04628-307">Click **Enable** on hello **SQL Server Settings** blade.</span></span>

![啟用 SQL Server R 服務](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a><span data-ttu-id="04628-309">5.檢閱 hello 摘要</span><span class="sxs-lookup"><span data-stu-id="04628-309">5. Review hello summary</span></span>
<span data-ttu-id="04628-310">在 hello**摘要**刀鋒視窗中，檢閱 hello 摘要，並按一下**確定** toocreate SQL Server、 資源群組和資源指定此 vm。</span><span class="sxs-lookup"><span data-stu-id="04628-310">On hello **Summary** blade, review hello summary and click **OK** toocreate SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="04628-311">您可以監視 hello 部署從 hello azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="04628-311">You can monitor hello deployment from hello azure portal.</span></span> <span data-ttu-id="04628-312">hello**通知**在 hello 囉 」 畫面最上方的按鈕會顯示 hello 部署的基本狀態。</span><span class="sxs-lookup"><span data-stu-id="04628-312">hello **Notifications** button at hello top of hello screen shows basic status of hello deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="04628-313">tooprovide 與了解部署時間，我以預設設定部署的 SQL VM toohello 美東地區。</span><span class="sxs-lookup"><span data-stu-id="04628-313">tooprovide you with an idea on deployment times, I deployed a SQL VM toohello East US region with default settings.</span></span> <span data-ttu-id="04628-314">此測試部署花費了 26 分鐘 toocomplete 總數。</span><span class="sxs-lookup"><span data-stu-id="04628-314">This test deployment took a total of 26 minutes toocomplete.</span></span> <span data-ttu-id="04628-315">但是根據您的區域和選取的設定，您可能會經歷較快或較慢的部署時間。</span><span class="sxs-lookup"><span data-stu-id="04628-315">But you might experience a faster or slower deployment time based on your region and selected settings.</span></span>
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a><span data-ttu-id="04628-316">使用遠端桌面開啟 hello VM</span><span class="sxs-lookup"><span data-stu-id="04628-316">Open hello VM with Remote Desktop</span></span>
<span data-ttu-id="04628-317">使用下列步驟 tooconnect toohello 虛擬機器使用遠端桌面的 hello:</span><span class="sxs-lookup"><span data-stu-id="04628-317">Use hello following steps tooconnect toohello virtual machine with Remote Desktop:</span></span>

1. <span data-ttu-id="04628-318">建立 Azure VM 的 hello hello hello 圖示 VM 就會出現 Azure 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="04628-318">After hello Azure VM is built, hello icon for hello VM appears on your Azure dashboard.</span></span> <span data-ttu-id="04628-319">瀏覽現有的虛擬機器，也可以找到它。</span><span class="sxs-lookup"><span data-stu-id="04628-319">You can also find it by browsing your existing virtual machines.</span></span> <span data-ttu-id="04628-320">按一下新的 SQL 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04628-320">Click on your new SQL virtual machine.</span></span> <span data-ttu-id="04628-321">[虛擬機器]  刀鋒視窗會顯示您的虛擬機器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="04628-321">A **Virtual machine** blade displays your virtual machine details.</span></span>
2. <span data-ttu-id="04628-322">頂端的 hello hello**虛擬機器**刀鋒視窗中，按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="04628-322">At hello top of hello **Virtual machine** blade, click **Connect**.</span></span>
3. <span data-ttu-id="04628-323">hello 瀏覽器下載 hello VM 的 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="04628-323">hello browser downloads an RDP file for hello VM.</span></span> <span data-ttu-id="04628-324">開啟 hello RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="04628-324">Open hello RDP file.</span></span>
    <span data-ttu-id="04628-325">![遠端桌面 tooSQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span><span class="sxs-lookup"><span data-stu-id="04628-325">![Remote Desktop tooSQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span></span>
4. <span data-ttu-id="04628-326">hello 遠端桌面連線會通知您該 hello 無法識別此遠端連線的發行者。</span><span class="sxs-lookup"><span data-stu-id="04628-326">hello Remote Desktop Connection notifies you that hello publisher of this remote connection cannot be identified.</span></span> <span data-ttu-id="04628-327">按一下**連接**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="04628-327">Click **Connect** toocontinue.</span></span>
5. <span data-ttu-id="04628-328">在 hello **Windows 安全性** 對話方塊中，按一下 **使用其他帳戶**。</span><span class="sxs-lookup"><span data-stu-id="04628-328">In hello **Windows Security** dialog, click **Use another account**.</span></span>
6. <span data-ttu-id="04628-329">如**使用者名**類型**\<使用者名稱 >**，其中<user name>是您指定當您設定 hello VM hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="04628-329">For **User name** type **\<user name>**, where <user name> is hello user name that you specified when you configured hello VM.</span></span> <span data-ttu-id="04628-330">您有 tooadd hello 名稱之前初始反斜線。</span><span class="sxs-lookup"><span data-stu-id="04628-330">You have tooadd an initial backslash before hello name.</span></span>
7. <span data-ttu-id="04628-331">型別 hello**密碼**，您先前針對這個 VM，然後按一下**確定**tooconnect。</span><span class="sxs-lookup"><span data-stu-id="04628-331">Type hello **Password** that you previously configured for this VM, and then click **OK** tooconnect.</span></span>
8. <span data-ttu-id="04628-332">如果另一個**遠端桌面連線**對話方塊詢問您是否 tooconnect，按一下 **是**。</span><span class="sxs-lookup"><span data-stu-id="04628-332">If another **Remote Desktop Connection** dialog asks you whether tooconnect, click **Yes**.</span></span>

<span data-ttu-id="04628-333">連接 toohello SQL Server 虛擬機器之後，您可以啟動 SQL Server Management Studio，並透過使用本機系統管理員認證的 Windows 驗證進行連接。</span><span class="sxs-lookup"><span data-stu-id="04628-333">After you connect toohello SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="04628-334">如果您啟用 SQL Server 驗證時，您也可以連接與 hello SQL 登入和密碼在佈建您已設定使用 SQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="04628-334">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using hello SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="04628-335">存取 toohello 電腦可讓您 toodirectly 變更電腦和您的需求為基礎的 SQL Server 設定。</span><span class="sxs-lookup"><span data-stu-id="04628-335">Access toohello machine enables you toodirectly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="04628-336">例如，您無法設定 hello 防火牆設定或變更 SQL Server 組態設定。</span><span class="sxs-lookup"><span data-stu-id="04628-336">For example, you could configure hello firewall settings or change SQL Server configuration settings.</span></span>

## <a name="connect-toosql-server-remotely"></a><span data-ttu-id="04628-337">從遠端連線 tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="04628-337">Connect tooSQL Server remotely</span></span>
<span data-ttu-id="04628-338">在本教學課程中，我們選取 **公用**hello 虛擬機器的存取和**SQL Server 驗證**。</span><span class="sxs-lookup"><span data-stu-id="04628-338">In this tutorial, we selected **Public** access for hello virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="04628-339">這些設定會自動設定的 hello 的虛擬機器 tooallow SQL Server 連線從任何用戶端透過 hello 網際網路 （假設它們擁有 hello 正確的 SQL 登入）。</span><span class="sxs-lookup"><span data-stu-id="04628-339">These settings automatically configured hello virtual machine tooallow SQL Server connections from any client over hello internet (assuming they have hello correct SQL login).</span></span>

> [!NOTE]
> <span data-ttu-id="04628-340">如果您未選取公用期間佈建，則額外的步驟，就需要的 tooaccess 您的 SQL Server 執行個體，透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="04628-340">If you did not select Public during provisioning, then extra steps are required tooaccess your SQL Server instance over hello internet.</span></span> <span data-ttu-id="04628-341">如需詳細資訊，請參閱[連接 SQL Server 虛擬機器 tooa](virtual-machines-windows-sql-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-341">For more information, see  [Connect tooa SQL Server Virtual Machine](virtual-machines-windows-sql-connect.md).</span></span>
> 
> 

<span data-ttu-id="04628-342">hello 下列各節顯示如何在您從不同的電腦上的 VM 上的 tooconnect tooyour SQL Server 執行個體 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="04628-342">hello following sections show how tooconnect tooyour SQL Server instance on your VM from a different computer over hello internet.</span></span>

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="04628-343">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04628-343">Next Steps</span></span>
<span data-ttu-id="04628-344">如需在 Azure 中使用 SQL Server 的其他資訊，請參閱[Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)和 hello[常見問題集](virtual-machines-windows-sql-server-iaas-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="04628-344">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and hello [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>

<span data-ttu-id="04628-345">監看的 SQL Server 在 Azure 虛擬機器的視訊概觀， [Azure VM 是 SQL Server 2016 hello 最佳平台](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)。</span><span class="sxs-lookup"><span data-stu-id="04628-345">For a video overview of SQL Server on Azure Virtual Machines, watch [Azure VM is hello best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).</span></span>

<span data-ttu-id="04628-346">[瀏覽 hello 學習路徑](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/)Azure 虛擬機器上的 SQL server。</span><span class="sxs-lookup"><span data-stu-id="04628-346">[Explore hello Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span>

