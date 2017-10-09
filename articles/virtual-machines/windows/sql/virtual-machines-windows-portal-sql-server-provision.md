---
title: "SQL Server 虛擬機器 aaaProvision |Microsoft 文件"
description: "建立並使用 hello 入口網站在 Azure 中的 tooa SQL Server 虛擬機器連線。 本教學課程使用 hello Resource Manager 模式。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a><span data-ttu-id="bc5df-104">佈建 hello Azure 入口網站中的 SQL Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bc5df-104">Provision a SQL Server virtual machine in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc5df-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="bc5df-105">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="bc5df-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc5df-106">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="bc5df-107">此端對端教學課程會示範如何 toouse 會 hello Azure 入口網站 tooprovision 執行 SQL Server 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc5df-107">This end-to-end tutorial shows you how toouse hello Azure portal tooprovision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="bc5df-108">hello Azure 虛擬機器 (VM) 映像庫含有包含 Microsoft SQL Server 的數個映像。</span><span class="sxs-lookup"><span data-stu-id="bc5df-108">hello Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="bc5df-109">按幾下，您可以選取其中一個 hello SQL VM 映像從 hello 組件庫，並佈建 Azure 環境中。</span><span class="sxs-lookup"><span data-stu-id="bc5df-109">With a few clicks, you can select one of hello SQL VM images from hello gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="bc5df-110">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="bc5df-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="bc5df-111">從 hello 庫中選取的 SQL VM 映像</span><span class="sxs-lookup"><span data-stu-id="bc5df-111">Select a SQL VM image from hello gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="bc5df-112">設定並建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="bc5df-112">Configure and create hello VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="bc5df-113">使用遠端桌面開啟 hello VM</span><span class="sxs-lookup"><span data-stu-id="bc5df-113">Open hello VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="bc5df-114">從遠端連線 tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="bc5df-114">Connect tooSQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a><span data-ttu-id="bc5df-115">從 hello 庫中選取的 SQL VM 映像</span><span class="sxs-lookup"><span data-stu-id="bc5df-115">Select a SQL VM image from hello gallery</span></span>

1. <span data-ttu-id="bc5df-116">登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc5df-116">Log in toohello [Azure portal](https://portal.azure.com) using your account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc5df-117">如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-117">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

2. <span data-ttu-id="bc5df-118">在 hello Azure 入口網站，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-118">On hello Azure portal, click **New**.</span></span> <span data-ttu-id="bc5df-119">hello 入口網站開啟 hello**新增**視窗。</span><span class="sxs-lookup"><span data-stu-id="bc5df-119">hello portal opens hello **New** window.</span></span>

3. <span data-ttu-id="bc5df-120">在 hello**新增**視窗中，按一下**計算**，然後按一下**查看所有**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-120">In hello **New** window, click **Compute** and then click **See all**.</span></span>

   ![新增計算視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. <span data-ttu-id="bc5df-122">在 hello 搜尋欄位中，輸入**SQL Server**，然後按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="bc5df-122">In hello search field, type **SQL Server**, and press ENTER.</span></span>

5. <span data-ttu-id="bc5df-123">然後按一下 hello**篩選**圖示，然後選擇**Microsoft** hello 發行者。</span><span class="sxs-lookup"><span data-stu-id="bc5df-123">Then click hello **Filter** icon and select **Microsoft** for hello publisher.</span></span> <span data-ttu-id="bc5df-124">按一下**完成**hello 篩選視窗 toofilter hello 結果 tooMicrosoft 發行 SQL Server 映像。</span><span class="sxs-lookup"><span data-stu-id="bc5df-124">Click **Done** on hello filter window toofilter hello results tooMicrosoft published SQL Server images.</span></span>

   ![Azure 虛擬機器視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="bc5df-126">檢閱 hello 可用的 SQL Server 映像。</span><span class="sxs-lookup"><span data-stu-id="bc5df-126">Review hello available SQL Server images.</span></span> <span data-ttu-id="bc5df-127">每個映像皆識別一個 SQL Server 版本和一個作業系統。</span><span class="sxs-lookup"><span data-stu-id="bc5df-127">Each image identifies a SQL Server version and an operating system.</span></span>

6. <span data-ttu-id="bc5df-128">名為選取的 hello 映像**免費授權： 在 Windows Server 2016 SQL Server 2016 SP1 Developer**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-128">Select hello image named **Free License: SQL Server 2016 SP1 Developer on Windows Server 2016**.</span></span>

   > [!TIP]
   > <span data-ttu-id="bc5df-129">hello Developer edition 會使用在本教學課程中，因為它是免費提供給開發測試用途的 SQL server 完整版本。</span><span class="sxs-lookup"><span data-stu-id="bc5df-129">hello Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes.</span></span> <span data-ttu-id="bc5df-130">您需支付只執行 hello VM hello 成本。</span><span class="sxs-lookup"><span data-stu-id="bc5df-130">You pay only for hello cost of running hello VM.</span></span> <span data-ttu-id="bc5df-131">不過，您必須可用 toochoose 任何 hello 映像 toouse 在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="bc5df-131">However, you are free toochoose any of hello images toouse in this tutorial.</span></span>

   > [!TIP]
   > <span data-ttu-id="bc5df-132">SQL VM 映像併入 hello 授權成本 for SQL Server hello 每分鐘定價的 hello （除了 hello developer Edition 和 Express edition) 您建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="bc5df-132">SQL VM images include hello licensing costs for SQL Server into hello per-minute pricing of hello VM you create (except for hello Developer and Express editions).</span></span> <span data-ttu-id="bc5df-133">SQL Server Developer 免費供開發/測試 (非生產環境) 使用，SQL Express 免費供輕量型工作負載 (少於 1GB 記憶體、小於 10 GB 儲存體) 使用。</span><span class="sxs-lookup"><span data-stu-id="bc5df-133">SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1GB memory, less than 10 GB storage).</span></span> <span data-ttu-id="bc5df-134">還有另一個選項 toobring 您-擁有的授權 (BYOL) 和 hello VM 工資。</span><span class="sxs-lookup"><span data-stu-id="bc5df-134">There is another option toobring-your-own-license (BYOL) and pay only for hello VM.</span></span> <span data-ttu-id="bc5df-135">這些映像的名稱前面會有 {BYOL}。</span><span class="sxs-lookup"><span data-stu-id="bc5df-135">Those image names are prefixed with {BYOL}.</span></span> 
   >
   > <span data-ttu-id="bc5df-136">如需這些選項的詳細資訊，請參閱 [SQL Server Azure VM 的定價指導方針](virtual-machines-windows-sql-server-pricing-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-136">For more information on these options, see [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

7. <span data-ttu-id="bc5df-137">在 [選取部署模型] 底下，確認已選取 [Resource Manager]。</span><span class="sxs-lookup"><span data-stu-id="bc5df-137">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="bc5df-138">資源管理員是 hello 建議新的虛擬機器的部署模型。</span><span class="sxs-lookup"><span data-stu-id="bc5df-138">Resource Manager is hello recommended deployment model for new virtual machines.</span></span> 

8. <span data-ttu-id="bc5df-139">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-139">Click **Create**.</span></span>

    ![使用 Resource Manager 建立 SQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a><span data-ttu-id="bc5df-141">設定 hello VM</span><span class="sxs-lookup"><span data-stu-id="bc5df-141">Configure hello VM</span></span>
<span data-ttu-id="bc5df-142">有五個視窗可用來設定 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc5df-142">There are five windows for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="bc5df-143">步驟</span><span class="sxs-lookup"><span data-stu-id="bc5df-143">Step</span></span> | <span data-ttu-id="bc5df-144">說明</span><span class="sxs-lookup"><span data-stu-id="bc5df-144">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bc5df-145">**基本概念**</span><span class="sxs-lookup"><span data-stu-id="bc5df-145">**Basics**</span></span> |[<span data-ttu-id="bc5df-146">設定基本設定</span><span class="sxs-lookup"><span data-stu-id="bc5df-146">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="bc5df-147">**大小**</span><span class="sxs-lookup"><span data-stu-id="bc5df-147">**Size**</span></span> |[<span data-ttu-id="bc5df-148">選擇虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="bc5df-148">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="bc5df-149">**設定**</span><span class="sxs-lookup"><span data-stu-id="bc5df-149">**Settings**</span></span> |[<span data-ttu-id="bc5df-150">設定選用功能</span><span class="sxs-lookup"><span data-stu-id="bc5df-150">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="bc5df-151">**SQL Server 設定**</span><span class="sxs-lookup"><span data-stu-id="bc5df-151">**SQL Server settings**</span></span> |[<span data-ttu-id="bc5df-152">進行 SQL Server 設定</span><span class="sxs-lookup"><span data-stu-id="bc5df-152">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="bc5df-153">**摘要**</span><span class="sxs-lookup"><span data-stu-id="bc5df-153">**Summary**</span></span> |[<span data-ttu-id="bc5df-154">檢閱 hello 摘要</span><span class="sxs-lookup"><span data-stu-id="bc5df-154">Review hello summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="bc5df-155">1.設定基本設定</span><span class="sxs-lookup"><span data-stu-id="bc5df-155">1. Configure basic settings</span></span>

<span data-ttu-id="bc5df-156">在 hello**基本概念**視窗中，提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc5df-156">On hello **Basics** window, provide hello following information:</span></span>

* <span data-ttu-id="bc5df-157">輸入唯一的虛擬機器 [名稱] 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-157">Enter a unique virtual machine **Name**.</span></span>

* <span data-ttu-id="bc5df-158">選取 **SSD** 作為 VM 磁碟類型，以獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="bc5df-158">Select **SSD** for VM disk type for optimal performance.</span></span>

* <span data-ttu-id="bc5df-159">指定**使用者名**hello hello VM 上的本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc5df-159">Specify a **User name** for hello local administrator account on hello VM.</span></span> <span data-ttu-id="bc5df-160">此帳戶也會加入 SQL Server toohello **sysadmin**固定的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="bc5df-160">This account is also added toohello SQL Server **sysadmin** fixed server role.</span></span>

* <span data-ttu-id="bc5df-161">提供強式 [密碼] 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-161">Provide a strong **Password**.</span></span>

* <span data-ttu-id="bc5df-162">如果您有多個訂閱，請確認 hello 訂用帳戶的正確 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="bc5df-162">If you have multiple subscriptions, verify that hello subscription is correct for hello new VM.</span></span>

* <span data-ttu-id="bc5df-163">在 hello**資源群組**方塊中，輸入新的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc5df-163">In hello **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="bc5df-164">或者，toouse 現有的資源群組按一下**使用現有**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-164">Alternatively, toouse an existing resource group click **Use existing**.</span></span> <span data-ttu-id="bc5df-165">資源群組是 Azure (虛擬機器、儲存體帳戶、虛擬網路等) 中相關資源的集合。</span><span class="sxs-lookup"><span data-stu-id="bc5df-165">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>

  > [!NOTE]
  > <span data-ttu-id="bc5df-166">如果您只是測試或了解 Azure 中的 SQL Server 部署，使用新的資源群組很有幫助。</span><span class="sxs-lookup"><span data-stu-id="bc5df-166">Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure.</span></span> <span data-ttu-id="bc5df-167">完成測試之後，刪除 hello 資源群組 tooautomatically 刪除 hello VM 和資源群組相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="bc5df-167">After you finish with your test, delete hello resource group tooautomatically delete hello VM and all resources associated with that resource group.</span></span> <span data-ttu-id="bc5df-168">如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-168">For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).</span></span>

* <span data-ttu-id="bc5df-169">選取**位置**hello 將要裝載此部署的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="bc5df-169">Select a **Location** for hello Azure region that will host this deployment.</span></span>

* <span data-ttu-id="bc5df-170">按一下**確定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="bc5df-170">Click **OK** toosave hello settings.</span></span>

    ![SQL 基本概念視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="bc5df-172">2.選擇虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="bc5df-172">2. Choose virtual machine size</span></span>

<span data-ttu-id="bc5df-173">在 hello**大小**步驟中，虛擬機器大小選擇 「 在 hello**大小選擇 「**視窗。</span><span class="sxs-lookup"><span data-stu-id="bc5df-173">On hello **Size** step, choose a virtual machine size in hello **Choose a size** window.</span></span> <span data-ttu-id="bc5df-174">hello 視窗一開始會顯示您選取的 hello 映像為基礎的建議的機器大小。</span><span class="sxs-lookup"><span data-stu-id="bc5df-174">hello window initially displays recommended machine sizes based on hello image you selected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc5df-175">hello 估計 hello 上顯示的每月成本**大小選擇 「**視窗不包含 SQL Server 授權成本。</span><span class="sxs-lookup"><span data-stu-id="bc5df-175">hello estimated monthly cost displayed on hello **Choose a size** window does not include SQL Server licensing costs.</span></span> <span data-ttu-id="bc5df-176">這是 hello VM 單獨 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="bc5df-176">This is hello cost of hello VM alone.</span></span> <span data-ttu-id="bc5df-177">Hello Express 和 Developer edition 的 SQL Server，這是 hello 總估計的成本。</span><span class="sxs-lookup"><span data-stu-id="bc5df-177">For hello Express and Developer editions of SQL Server, this is hello total estimated cost.</span></span> <span data-ttu-id="bc5df-178">對於其他版本，請參閱 hello [Windows 虛擬機器定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)並選取您目標的 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="bc5df-178">For other editions, see hello [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server.</span></span> <span data-ttu-id="bc5df-179">另請參閱 hello[定價指導方針 SQL Server 的 Azure Vm](virtual-machines-windows-sql-server-pricing-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-179">Also see hello [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

![SQL VM 大小選項](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="bc5df-181">對於生產工作負載，請參閱 hello 建議機器大小和組態中的[Azure 虛擬機器中 SQL Server 的效能最佳做法](virtual-machines-windows-sql-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-181">For production workloads, see hello recommended machine sizes and configuration in [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span> <span data-ttu-id="bc5df-182">如果您需要未列出的機器大小，請按一下 hello**檢視所有** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bc5df-182">If you need a machine size that is not listed, click hello **View all** button.</span></span>

> [!NOTE]
> <span data-ttu-id="bc5df-183">如需關於虛擬機器大小的詳細資訊，請參閱 [虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-183">For more information about virtual machine sizes see, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="bc5df-184">選擇您的機器大小，然後按一下選取 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-184">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="bc5df-185">3.設定選用功能</span><span class="sxs-lookup"><span data-stu-id="bc5df-185">3. Configure optional features</span></span>

<span data-ttu-id="bc5df-186">在 hello**設定**視窗中，設定 Azure 儲存體、 網路功能與監視 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc5df-186">On hello **Settings** window, configure Azure storage, networking, and monitoring for hello virtual machine.</span></span>

* <span data-ttu-id="bc5df-187">在 [儲存體] 之下，選取 [是] 以使用 [受控磁碟]。</span><span class="sxs-lookup"><span data-stu-id="bc5df-187">Under **Storage**, select **Yes** under use **Managed Disks**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc5df-188">Microsoft 建議使用 SQL Server 適用的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="bc5df-188">Microsoft recommends Managed Disks for SQL Server.</span></span> <span data-ttu-id="bc5df-189">管理磁碟 hello 幕後的控制代碼儲存體。</span><span class="sxs-lookup"><span data-stu-id="bc5df-189">Managed Disks handles storage behind hello scenes.</span></span> <span data-ttu-id="bc5df-190">此外，當與受管理磁碟的虛擬機器都處於 hello 相同可用性設定組，Azure 會發佈 hello 存放裝置資源 tooprovide 適當備援。</span><span class="sxs-lookup"><span data-stu-id="bc5df-190">In addition, when virtual machines with Managed Disks are in hello same availability set, Azure distributes hello storage resources tooprovide appropriate redundancy.</span></span> <span data-ttu-id="bc5df-191">如需其他資訊，請參閱 [Azure 受控磁碟概觀 (英文)](../../../storage/storage-managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-191">For additional information, see [Azure Managed Disks Overview](../../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="bc5df-192">如需可用性設定組中受控磁碟的具體資訊，請參閱[在可用性設定組中使用 VM 的受控磁碟](../manage-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-192">For specifics about managed disks in an availability set, see [Use managed disks for VMs in availability set](../manage-availability.md).</span></span>

* <span data-ttu-id="bc5df-193">在下**網路**，您可以接受 hello 自動填入值。</span><span class="sxs-lookup"><span data-stu-id="bc5df-193">Under **Network**, you can accept hello automatically populated values.</span></span> <span data-ttu-id="bc5df-194">您也可以按一下每個功能 toomanually 設定 hello**虛擬網路**，**子網路**，**公用 IP 位址**，和**網路安全性群組**.</span><span class="sxs-lookup"><span data-stu-id="bc5df-194">You can also click on each feature toomanually configure hello **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="bc5df-195">基於 hello 本教學課程中，保留 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="bc5df-195">For hello purposes of this tutorial, keep hello default values.</span></span>

* <span data-ttu-id="bc5df-196">Azure 可讓**監視**預設與 hello hello VM 為指定的相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc5df-196">Azure enables **Monitoring** by default with hello same storage account designated for hello VM.</span></span> <span data-ttu-id="bc5df-197">您可以在這裡變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="bc5df-197">You can change these settings here.</span></span>

* <span data-ttu-id="bc5df-198">在下**可用性設定組**，您可以保留 hello 預設值是**無**本教學課程。</span><span class="sxs-lookup"><span data-stu-id="bc5df-198">Under **Availability set**, you can leave hello default of **none** for this tutorial.</span></span> <span data-ttu-id="bc5df-199">如果您計劃 tooset SQL AlwaysOn 可用性群組上的，設定 hello 可用性 tooavoid 重建 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc5df-199">If you plan tooset up SQL AlwaysOn Availability Groups, configure hello availability tooavoid recreating hello virtual machine.</span></span>  <span data-ttu-id="bc5df-200">如需詳細資訊，請參閱[管理 hello 虛擬機器可用性](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-200">For more information, see [Manage hello Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="bc5df-201">完成這些設定時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-201">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="bc5df-202">4.進行 SQL Server 設定</span><span class="sxs-lookup"><span data-stu-id="bc5df-202">4. Configure SQL server settings</span></span>
<span data-ttu-id="bc5df-203">在 hello **SQL Server 設定**視窗中，設定特定的設定和針對 SQL Server 最佳化。</span><span class="sxs-lookup"><span data-stu-id="bc5df-203">On hello **SQL Server settings** window, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="bc5df-204">您可以設定 SQL Server 的 hello 設定 hello 如下。</span><span class="sxs-lookup"><span data-stu-id="bc5df-204">hello settings that you can configure for SQL Server include hello following.</span></span>

| <span data-ttu-id="bc5df-205">設定</span><span class="sxs-lookup"><span data-stu-id="bc5df-205">Setting</span></span> |
| --- |
| [<span data-ttu-id="bc5df-206">連線能力</span><span class="sxs-lookup"><span data-stu-id="bc5df-206">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="bc5df-207">驗證</span><span class="sxs-lookup"><span data-stu-id="bc5df-207">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="bc5df-208">儲存體組態</span><span class="sxs-lookup"><span data-stu-id="bc5df-208">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="bc5df-209">自動修補</span><span class="sxs-lookup"><span data-stu-id="bc5df-209">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="bc5df-210">自動備份</span><span class="sxs-lookup"><span data-stu-id="bc5df-210">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="bc5df-211">Azure 金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="bc5df-211">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="bc5df-212">R 服務</span><span class="sxs-lookup"><span data-stu-id="bc5df-212">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="bc5df-213">連線能力</span><span class="sxs-lookup"><span data-stu-id="bc5df-213">Connectivity</span></span>

<span data-ttu-id="bc5df-214">在下**SQL 連接性**，指定 hello 類型要 toohello 這部 vm 的 SQL Server 執行個體的存取。</span><span class="sxs-lookup"><span data-stu-id="bc5df-214">Under **SQL connectivity**, specify hello type of access you want toohello SQL Server instance on this VM.</span></span> <span data-ttu-id="bc5df-215">基於 hello 本教學課程中，選取**公用 （網際網路）**從機器或服務上的 tooallow 連線 tooSQL 伺服器 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="bc5df-215">For hello purposes of this tutorial, select **Public (internet)** tooallow connections tooSQL Server from machines or services on hello internet.</span></span> <span data-ttu-id="bc5df-216">選取此選項，Azure 會自動設定 hello 防火牆與 hello 網路安全性的群組 tooallow 流量通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="bc5df-216">With this option selected, Azure automatically configures hello firewall and hello network security group tooallow traffic on port 1433.</span></span>

![SQL 連線選項](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> <span data-ttu-id="bc5df-218">根據預設，SQL Server 會在已知通訊埠 **1433** 上接聽。</span><span class="sxs-lookup"><span data-stu-id="bc5df-218">By default, SQL Server listens on a well-known port, **1433**.</span></span> <span data-ttu-id="bc5df-219">為了提高安全性，變更在非預設通訊埠，例如 1401 hello 先前對話方塊 toolisten hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="bc5df-219">For increased security, change hello port in hello previous dialog toolisten on a non-default port, such as 1401.</span></span> <span data-ttu-id="bc5df-220">如果您這麼做，您必須使用該連接埠從任何用戶端工具 (例如 SSMS) 進行連線。</span><span class="sxs-lookup"><span data-stu-id="bc5df-220">If you do this, you must connect using that port from any client tools, such as SSMS.</span></span>

<span data-ttu-id="bc5df-221">tooconnect tooSQL 伺服器 hello 透過網際網路，您也必須啟用 SQL Server 驗證，hello 下一節中所述。</span><span class="sxs-lookup"><span data-stu-id="bc5df-221">tooconnect tooSQL Server via hello internet, you also must enable SQL Server Authentication, which is described in hello next section.</span></span>

<span data-ttu-id="bc5df-222">如果您希望 Database Engine toonot 啟用連線 toohello 透過 hello 網際網路，選擇其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="bc5df-222">If you would prefer toonot enable connections toohello Database Engine via hello internet, choose one of hello following options:</span></span>

* <span data-ttu-id="bc5df-223">**（在 VM 只) 內本機**tooallow 連線 tooSQL 只能從伺服器 hello VM 內。</span><span class="sxs-lookup"><span data-stu-id="bc5df-223">**Local (inside VM only)** tooallow connections tooSQL Server only from within hello VM.</span></span>
* <span data-ttu-id="bc5df-224">**（在虛擬網路） 內的私用**從機器或服務在 hello tooallow 連線 tooSQL 伺服器相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bc5df-224">**Private (within Virtual Network)** tooallow connections tooSQL Server from machines or services in hello same virtual network.</span></span>

<span data-ttu-id="bc5df-225">一般情況下，選擇 hello 限制最嚴格連線能力，可讓您的案例來改善安全性。</span><span class="sxs-lookup"><span data-stu-id="bc5df-225">In general, improve security by choosing hello most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="bc5df-226">但所有 hello 選項都會透過網路安全性群組規則和 SQL/Windows 驗證安全性實體。</span><span class="sxs-lookup"><span data-stu-id="bc5df-226">But all hello options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span> <span data-ttu-id="bc5df-227">Hello 建立 VM 之後，您可以編輯網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="bc5df-227">You can edit Network Security Group after hello VM is created.</span></span> <span data-ttu-id="bc5df-228">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 安全性考量](virtual-machines-windows-sql-security.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-228">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bc5df-229">適用於 SQL Server Express edition 的 hello 虛擬機器映像不會自動啟用 hello TCP/IP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="bc5df-229">hello virtual machine image for SQL Server Express edition does not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="bc5df-230">這是即使的 hello 公用與私人連線，則為 true 的選項。</span><span class="sxs-lookup"><span data-stu-id="bc5df-230">This is true even for hello Public and  Private connectivity options.</span></span> <span data-ttu-id="bc5df-231">Express 版本中，您必須用於 SQL Server 組態管理員太[手動啟用 hello TCP/IP 通訊協定](#configure-sql-server-to-listen-on-the-tcp-protocol)之後建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="bc5df-231">For Express edition, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating hello VM.</span></span>

### <a name="authentication"></a><span data-ttu-id="bc5df-232">驗證</span><span class="sxs-lookup"><span data-stu-id="bc5df-232">Authentication</span></span>

<span data-ttu-id="bc5df-233">如果您需要「SQL Server 驗證」，請按一下 [SQL 驗證]  under 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-233">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![SQL Server 驗證](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> <span data-ttu-id="bc5df-235">如果您打算 tooaccess SQL Server 透過 hello 網際網路 (也就是 hello 公用連線選項)，您必須啟用 SQL 驗證這裡。</span><span class="sxs-lookup"><span data-stu-id="bc5df-235">If you plan tooaccess SQL Server over hello internet (i.e. hello Public connectivity option), you must enable SQL authentication here.</span></span> <span data-ttu-id="bc5df-236">SQL Server 的公用存取 toohello 需要 hello 使用 SQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="bc5df-236">Public access toohello SQL Server requires hello use of SQL Authentication.</span></span>
> 
> 

<span data-ttu-id="bc5df-237">如果您啟用 [SQL Server 驗證]，請指定 [登入名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="bc5df-237">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="bc5df-238">這個使用者名稱設定為 SQL Server 驗證登入和成員的 hello **sysadmin**固定的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="bc5df-238">This user name is configured as a SQL Server Authentication login and member of hello **sysadmin** fixed server role.</span></span> <span data-ttu-id="bc5df-239">如需有關「驗證模式」的詳細資訊，請參閱 [選擇驗證模式](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-239">See [Choose an Authentication Mode](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) for more information about Authentication Modes.</span></span>

<span data-ttu-id="bc5df-240">如果您未啟用 SQL Server 驗證，然後您就可以使用本機系統管理員帳戶 hello hello VM tooconnect toohello SQL Server 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="bc5df-240">If you do not enable SQL Server Authentication, then you can use hello local Administrator account on hello VM tooconnect toohello SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="bc5df-241">儲存體組態</span><span class="sxs-lookup"><span data-stu-id="bc5df-241">Storage configuration</span></span>

<span data-ttu-id="bc5df-242">按一下**儲存體設定**toospecify hello 存放裝置需求。</span><span class="sxs-lookup"><span data-stu-id="bc5df-242">Click **Storage configuration** toospecify hello storage requirements.</span></span>

![SQL 儲存體組態](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> <span data-ttu-id="bc5df-244">如果您手動設定 VM toouse 標準存放裝置，此選項無法使用。</span><span class="sxs-lookup"><span data-stu-id="bc5df-244">If you manually configured your VM toouse standard storage, this option is not available.</span></span> <span data-ttu-id="bc5df-245">自動儲存體最佳化只適用於進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="bc5df-245">Automatic storage optimization is available only for Premium Storage.</span></span>

> [!TIP]
> <span data-ttu-id="bc5df-246">hello 停駐點的數目和每個滑桿的 hello 上限會相依於 hello 您選取的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="bc5df-246">hello number of stops and hello upper limits of each slider is dependent on hello size of VM you selected.</span></span> <span data-ttu-id="bc5df-247">較大且更強大的 VM 是無法 tooscale 上。</span><span class="sxs-lookup"><span data-stu-id="bc5df-247">A larger and more powerful VM is able tooscale up more.</span></span>

<span data-ttu-id="bc5df-248">您可以用每秒輸入/輸出作業數 (IOPs)、輸送量 (單位為 MB/s) 及總儲存體大小來指定需求。</span><span class="sxs-lookup"><span data-stu-id="bc5df-248">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="bc5df-249">使用 hello 滑動縮放比例，以設定這些值。</span><span class="sxs-lookup"><span data-stu-id="bc5df-249">Configure these values by using hello sliding scales.</span></span> <span data-ttu-id="bc5df-250">您可以根據工作負載變更這些儲存體設定。</span><span class="sxs-lookup"><span data-stu-id="bc5df-250">You can change these storage settings based on workload.</span></span> <span data-ttu-id="bc5df-251">hello 入口網站會自動計算 hello 磁碟 tooattach 數目，並設定根據這些需求。</span><span class="sxs-lookup"><span data-stu-id="bc5df-251">hello portal automatically calculates hello number of disks tooattach and configure based on these requirements.</span></span>

<span data-ttu-id="bc5df-252">在下**針對儲存體最佳化**，選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="bc5df-252">Under **Storage optimized for**, select one of hello following options:</span></span>

* <span data-ttu-id="bc5df-253">**一般**hello 預設設定，並且支援大部分的工作負載。</span><span class="sxs-lookup"><span data-stu-id="bc5df-253">**General** is hello default setting and supports most workloads.</span></span>
* <span data-ttu-id="bc5df-254">**交易式**傳統資料庫 OLTP 工作負載的 hello 儲存體的處理最佳化。</span><span class="sxs-lookup"><span data-stu-id="bc5df-254">**Transactional** processing optimizes hello storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="bc5df-255">**資料倉儲**hello 儲存體分析和報告工作負載最佳化。</span><span class="sxs-lookup"><span data-stu-id="bc5df-255">**Data warehousing** optimizes hello storage for analytic and reporting workloads.</span></span>

### <a name="automated-patching"></a><span data-ttu-id="bc5df-256">自動修補</span><span class="sxs-lookup"><span data-stu-id="bc5df-256">Automated patching</span></span>

<span data-ttu-id="bc5df-257">**Automated patching** 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-257">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="bc5df-258">自動修補允許 Azure tooautomatically 修補 SQL Server 和 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="bc5df-258">Automated patching allows Azure tooautomatically patch SQL Server and hello operating system.</span></span> <span data-ttu-id="bc5df-259">指定一天的 hello 週、 時間和維護期間的持續時間。</span><span class="sxs-lookup"><span data-stu-id="bc5df-259">Specify a day of hello week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="bc5df-260">Azure 會在此維護期間執行修補。</span><span class="sxs-lookup"><span data-stu-id="bc5df-260">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="bc5df-261">hello 維護窗口排程會為時間使用 hello VM 地區設定。</span><span class="sxs-lookup"><span data-stu-id="bc5df-261">hello maintenance window schedule uses hello VM locale for time.</span></span> <span data-ttu-id="bc5df-262">如果不想使用 Azure tooautomatically 修補 SQL Server 和 hello 作業系統，請按一下**停用**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-262">If you do not want Azure tooautomatically patch SQL Server and hello operating system, click **Disable**.</span></span>  

![SQL 自動修補](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="bc5df-264">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補](virtual-machines-windows-sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-264">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="bc5df-265">自動備份</span><span class="sxs-lookup"><span data-stu-id="bc5df-265">Automated backup</span></span>

<span data-ttu-id="bc5df-266">在 [自動備份] 底下，可以為所有資料庫啟用自動資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="bc5df-266">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="bc5df-267">預設會停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="bc5df-267">Automated backup is disabled by default.</span></span>

<span data-ttu-id="bc5df-268">當您啟用 SQL 自動的備份時，您可以設定下列 hello:</span><span class="sxs-lookup"><span data-stu-id="bc5df-268">When you enable SQL automated backup, you can configure hello following:</span></span>

* <span data-ttu-id="bc5df-269">備份的保留期限 (天數)</span><span class="sxs-lookup"><span data-stu-id="bc5df-269">Retention period (days) for backups</span></span>
* <span data-ttu-id="bc5df-270">備份的儲存體帳戶 toouse</span><span class="sxs-lookup"><span data-stu-id="bc5df-270">Storage account toouse for backups</span></span>
* <span data-ttu-id="bc5df-271">備份的加密選項和密碼</span><span class="sxs-lookup"><span data-stu-id="bc5df-271">Encryption option and password for backups</span></span>
* <span data-ttu-id="bc5df-272">備份系統資料庫</span><span class="sxs-lookup"><span data-stu-id="bc5df-272">Backup system databases</span></span>
* <span data-ttu-id="bc5df-273">設定備份排程</span><span class="sxs-lookup"><span data-stu-id="bc5df-273">Configure backup schedule</span></span>

<span data-ttu-id="bc5df-274">tooencrypt hello 備份、 按一下**啟用**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-274">tooencrypt hello backup, click **Enable**.</span></span> <span data-ttu-id="bc5df-275">然後指定 hello**密碼**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-275">Then specify hello **Password**.</span></span> <span data-ttu-id="bc5df-276">Azure 會建立憑證 tooencrypt hello 備份，並使用 hello 指定密碼 tooprotect 該憑證。</span><span class="sxs-lookup"><span data-stu-id="bc5df-276">Azure creates a certificate tooencrypt hello backups and uses hello specified password tooprotect that certificate.</span></span>

![SQL 自動備份](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="bc5df-278">如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的自動化備份](virtual-machines-windows-sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-278">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="bc5df-279">Azure 金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="bc5df-279">Azure Key Vault integration</span></span>

<span data-ttu-id="bc5df-280">按一下 toostore 安全性密碼，在 Azure 中的進行加密， **Azure 金鑰保存庫整合**按一下**啟用**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-280">toostore security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure 金鑰保存庫整合](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="bc5df-282">hello 下表列出 hello 參數需要的 tooconfigure Azure 金鑰保存庫整合。</span><span class="sxs-lookup"><span data-stu-id="bc5df-282">hello following table lists hello parameters required tooconfigure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="bc5df-283">參數</span><span class="sxs-lookup"><span data-stu-id="bc5df-283">PARAMETER</span></span> | <span data-ttu-id="bc5df-284">說明</span><span class="sxs-lookup"><span data-stu-id="bc5df-284">DESCRIPTION</span></span> | <span data-ttu-id="bc5df-285">範例</span><span class="sxs-lookup"><span data-stu-id="bc5df-285">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc5df-286">**金鑰保存庫 URL**</span><span class="sxs-lookup"><span data-stu-id="bc5df-286">**Key Vault URL**</span></span> |<span data-ttu-id="bc5df-287">hello hello 金鑰保存庫位置。</span><span class="sxs-lookup"><span data-stu-id="bc5df-287">hello location of hello key vault.</span></span> |<span data-ttu-id="bc5df-288">https://contosokeyvault.vault.azure.net/</span><span class="sxs-lookup"><span data-stu-id="bc5df-288">https://contosokeyvault.vault.azure.net/</span></span> |
| <span data-ttu-id="bc5df-289">**主體名稱**</span><span class="sxs-lookup"><span data-stu-id="bc5df-289">**Principal name**</span></span> |<span data-ttu-id="bc5df-290">Azure Active Directory 服務主體名稱。</span><span class="sxs-lookup"><span data-stu-id="bc5df-290">Azure Active Directory service principal name.</span></span> <span data-ttu-id="bc5df-291">此名稱也是參考的 tooas hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="bc5df-291">This name is also referred tooas hello Client ID.</span></span> |<span data-ttu-id="bc5df-292">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="bc5df-292">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="bc5df-293">**主體密碼**</span><span class="sxs-lookup"><span data-stu-id="bc5df-293">**Principal secret**</span></span> |<span data-ttu-id="bc5df-294">Azure Active Directory 服務主體密碼。</span><span class="sxs-lookup"><span data-stu-id="bc5df-294">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="bc5df-295">這個密碼也會參照的 tooas hello 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="bc5df-295">This secret is also referred tooas hello Client Secret.</span></span> |<span data-ttu-id="bc5df-296">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="bc5df-296">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="bc5df-297">**認證名稱**</span><span class="sxs-lookup"><span data-stu-id="bc5df-297">**Credential name**</span></span> |<span data-ttu-id="bc5df-298">**認證名稱**: AKV 整合建立 SQL Server，讓 hello VM toohave 存取 toohello 金鑰保存庫中的認證。</span><span class="sxs-lookup"><span data-stu-id="bc5df-298">**Credential name**: AKV Integration creates a credential within SQL Server, allowing hello VM toohave access toohello key vault.</span></span> <span data-ttu-id="bc5df-299">選擇此認證的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc5df-299">Choose a name for this credential.</span></span> |<span data-ttu-id="bc5df-300">mycred1</span><span class="sxs-lookup"><span data-stu-id="bc5df-300">mycred1</span></span> |

<span data-ttu-id="bc5df-301">如需詳細資訊，請參閱 [在 Azure VM 上設定 SQL Server 的 Azure 金鑰保存庫整合](virtual-machines-windows-ps-sql-keyvault.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-301">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

### <a name="r-services"></a><span data-ttu-id="bc5df-302">R 服務</span><span class="sxs-lookup"><span data-stu-id="bc5df-302">R services</span></span>

<span data-ttu-id="bc5df-303">您已擁有 hello 選項 tooenable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-303">You have hello option tooenable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="bc5df-304">這可讓您使用 SQL Server 2016 toouse 進階分析。</span><span class="sxs-lookup"><span data-stu-id="bc5df-304">This enables you toouse advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="bc5df-305">按一下**啟用**上 hello **SQL Server 設定**視窗。</span><span class="sxs-lookup"><span data-stu-id="bc5df-305">Click **Enable** on hello **SQL Server Settings** window.</span></span>

> [!NOTE]
> <span data-ttu-id="bc5df-306">SQL Server 2016 Developer edition，此選項會不正確地停用 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bc5df-306">For SQL Server 2016 Developer Edition, this option is incorrectly disabled by hello portal.</span></span> <span data-ttu-id="bc5df-307">對於 Developer Edition，您必須在建立 VM 之後手動啟用 R Services。</span><span class="sxs-lookup"><span data-stu-id="bc5df-307">For Developer edition, you must enable R Services manually after creating your VM.</span></span>

![啟用 SQL Server R 服務](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

<span data-ttu-id="bc5df-309">完成 SQL Server 設定之後，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bc5df-309">When you are finished configuring SQL Server settings, click **OK**.</span></span>

## <a name="5-review-hello-summary"></a><span data-ttu-id="bc5df-310">5.檢閱 hello 摘要</span><span class="sxs-lookup"><span data-stu-id="bc5df-310">5. Review hello summary</span></span>

<span data-ttu-id="bc5df-311">在 hello**摘要**視窗中，檢閱 hello 摘要，然後按一下**購買**toocreate SQL Server、 資源群組和資源指定此 vm。</span><span class="sxs-lookup"><span data-stu-id="bc5df-311">On hello **Summary** window, review hello summary and click **Purchase** toocreate SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="bc5df-312">您可以監視 hello 部署從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bc5df-312">You can monitor hello deployment from hello Azure portal.</span></span> <span data-ttu-id="bc5df-313">hello**通知**在 hello 囉 」 畫面最上方的按鈕會顯示 hello 部署的基本狀態。</span><span class="sxs-lookup"><span data-stu-id="bc5df-313">hello **Notifications** button at hello top of hello screen shows basic status of hello deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="bc5df-314">tooprovide 與了解部署時間，我以預設設定部署的 SQL VM toohello 美東地區。</span><span class="sxs-lookup"><span data-stu-id="bc5df-314">tooprovide you with an idea on deployment times, I deployed a SQL VM toohello East US region with default settings.</span></span> <span data-ttu-id="bc5df-315">此測試部署花費了 26 分鐘 toocomplete 總數。</span><span class="sxs-lookup"><span data-stu-id="bc5df-315">This test deployment took a total of 26 minutes toocomplete.</span></span> <span data-ttu-id="bc5df-316">但是根據您的區域和選取的設定，您可能會經歷較快或較慢的部署時間。</span><span class="sxs-lookup"><span data-stu-id="bc5df-316">But you might experience a faster or slower deployment time based on your region and selected settings.</span></span>

## <a name="open-hello-vm-with-remote-desktop"></a><span data-ttu-id="bc5df-317">使用遠端桌面開啟 hello VM</span><span class="sxs-lookup"><span data-stu-id="bc5df-317">Open hello VM with Remote Desktop</span></span>

<span data-ttu-id="bc5df-318">使用下列步驟 tooconnect toohello SQL Server 虛擬機器使用遠端桌面的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc5df-318">Use hello following steps tooconnect toohello SQL Server virtual machine with Remote Desktop:</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="bc5df-319">連接 toohello SQL Server 虛擬機器之後，您可以啟動 SQL Server Management Studio，並透過使用本機系統管理員認證的 Windows 驗證進行連接。</span><span class="sxs-lookup"><span data-stu-id="bc5df-319">After you connect toohello SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="bc5df-320">如果您啟用 SQL Server 驗證時，您也可以連接與 hello SQL 登入和密碼在佈建您已設定使用 SQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="bc5df-320">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using hello SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="bc5df-321">存取 toohello 電腦可讓您 toodirectly 變更電腦和您的需求為基礎的 SQL Server 設定。</span><span class="sxs-lookup"><span data-stu-id="bc5df-321">Access toohello machine enables you toodirectly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="bc5df-322">例如，您無法設定 hello 防火牆設定或變更 SQL Server 組態設定。</span><span class="sxs-lookup"><span data-stu-id="bc5df-322">For example, you could configure hello firewall settings or change SQL Server configuration settings.</span></span>

## <a name="enable-tcpip-for-developer-and-express-editions"></a><span data-ttu-id="bc5df-323">針對 Developer 和 Express 版本啟用 TCP/IP</span><span class="sxs-lookup"><span data-stu-id="bc5df-323">Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="bc5df-324">佈建時新的 SQL Server VM，Azure 不會自動啟用 hello TCP/IP 通訊協定的 SQL Server Developer edition 和 Express edition。</span><span class="sxs-lookup"><span data-stu-id="bc5df-324">When provisioning a new SQL Server VM, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="bc5df-325">hello 執行下列步驟說明如何 toomanually 啟用 TCP/IP 時，讓您可以從遠端連線的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="bc5df-325">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="bc5df-326">hello 下列步驟使用**SQL Server 組態管理員**tooenable hello TCP/IP 通訊協定的 SQL Server Developer edition 和 Express edition。</span><span class="sxs-lookup"><span data-stu-id="bc5df-326">hello following steps use **SQL Server Configuration Manager** tooenable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a><span data-ttu-id="bc5df-327">從遠端連線 tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="bc5df-327">Connect tooSQL Server remotely</span></span>

<span data-ttu-id="bc5df-328">在本教學課程中，我們選取 **公用**hello 虛擬機器的存取和**SQL Server 驗證**。</span><span class="sxs-lookup"><span data-stu-id="bc5df-328">In this tutorial, we selected **Public** access for hello virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="bc5df-329">這些設定會自動設定的 hello 的虛擬機器 tooallow SQL Server 連線從任何用戶端透過 hello 網際網路 （假設它們擁有 hello 正確的 SQL 登入）。</span><span class="sxs-lookup"><span data-stu-id="bc5df-329">These settings automatically configured hello virtual machine tooallow SQL Server connections from any client over hello internet (assuming they have hello correct SQL login).</span></span>

> [!NOTE]
> <span data-ttu-id="bc5df-330">如果您未選取公用佈建期間，您可以佈建之後變更您的 SQL 連線設定，透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bc5df-330">If you did not select Public during provisioning, then you can change your SQL connectivity settings through hello portal after provisioning.</span></span> <span data-ttu-id="bc5df-331">如需詳細資訊，請參閱[變更 SQL 連線設定](virtual-machines-windows-sql-connect.md#change)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-331">For more information, see  [Change your SQL connectivity settings](virtual-machines-windows-sql-connect.md#change).</span></span>

<span data-ttu-id="bc5df-332">hello 下列各節顯示如何在您從不同的電腦上的 VM 上的 tooconnect tooyour SQL Server 執行個體 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="bc5df-332">hello following sections show how tooconnect tooyour SQL Server instance on your VM from a different computer over hello internet.</span></span>

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="bc5df-333">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc5df-333">Next Steps</span></span>

<span data-ttu-id="bc5df-334">如需在 Azure 中使用 SQL Server 的其他資訊，請參閱[Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)和 hello[常見問題集](virtual-machines-windows-sql-server-iaas-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="bc5df-334">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and hello [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>
