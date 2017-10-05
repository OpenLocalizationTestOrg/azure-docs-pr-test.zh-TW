---
title: "佈建 SQL Server 虛擬機器 | Microsoft Docs"
description: "使用入口網站在 Azure 中建立並連接到 SQL Server 虛擬機器。 本教學課程會使用 Resource Manager 模式。"
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
ms.openlocfilehash: c51908058bb785cb33da21de76ba3c956b6b9f1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-the-azure-portal"></a><span data-ttu-id="51a9c-104">在 Azure 入口網站中佈建 SQL Server 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="51a9c-104">Provision a SQL Server virtual machine in the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="51a9c-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="51a9c-105">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="51a9c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51a9c-106">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="51a9c-107">本端對端教學課程將示範如何使用 Azure 入口網站佈建執行 SQL Server 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a9c-107">This end-to-end tutorial shows you how to use the Azure Portal to provision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="51a9c-108">Azure 虛擬機器 (VM) 資源庫涵蓋數個包含 Microsoft SQL Server 的映像。</span><span class="sxs-lookup"><span data-stu-id="51a9c-108">The Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="51a9c-109">只需按幾下，即可從資源庫中選取其中一個 VM 映像，並在您的 Azure 環境中加以佈建。</span><span class="sxs-lookup"><span data-stu-id="51a9c-109">With a few clicks, you can select one of the SQL VM images from the gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="51a9c-110">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="51a9c-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="51a9c-111">從資源庫中選取 SQL VM 映像</span><span class="sxs-lookup"><span data-stu-id="51a9c-111">Select a SQL VM image from the gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="51a9c-112">設定並建立 VM</span><span class="sxs-lookup"><span data-stu-id="51a9c-112">Configure and create the VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="51a9c-113">透過遠端桌面開啟 VM</span><span class="sxs-lookup"><span data-stu-id="51a9c-113">Open the VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="51a9c-114">從遠端連接到 SQL Server</span><span class="sxs-lookup"><span data-stu-id="51a9c-114">Connect to SQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-the-gallery"></a><span data-ttu-id="51a9c-115">從資源庫中選取 SQL VM 映像</span><span class="sxs-lookup"><span data-stu-id="51a9c-115">Select a SQL VM image from the gallery</span></span>
1. <span data-ttu-id="51a9c-116">使用您的帳戶登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-116">Log in to the [Azure portal](https://portal.azure.com) using your account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="51a9c-117">如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-117">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

2. <span data-ttu-id="51a9c-118">在 Azure 入口網站上，按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-118">On the Azure portal, click **New**.</span></span> <span data-ttu-id="51a9c-119">入口網站會開啟 [新增]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="51a9c-119">The portal opens the **New** blade.</span></span> <span data-ttu-id="51a9c-120">SQL Server VM 資源位於 Marketplace 的 [計算] 群組中。</span><span class="sxs-lookup"><span data-stu-id="51a9c-120">The SQL Server VM resources are in the **Compute** group of the Marketplace.</span></span>
3. <span data-ttu-id="51a9c-121">在 [新增] 刀鋒視窗中，按一下 [計算]，然後按一下 [檢視全部]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-121">In the **New** blade, click **Compute** and then click **See all**.</span></span>
4. <span data-ttu-id="51a9c-122">在 [篩選器] 文字方塊中，輸入 SQL Server，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="51a9c-122">In the **Filter** text box type SQL Server, and press the ENTER key.</span></span>

   ![Azure 虛擬機器刀鋒視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="51a9c-124">檢閱可用的 SQL Server 映像。</span><span class="sxs-lookup"><span data-stu-id="51a9c-124">Review the available SQL Server images.</span></span> <span data-ttu-id="51a9c-125">每個映像皆識別一個 SQL Server 版本和一個作業系統。</span><span class="sxs-lookup"><span data-stu-id="51a9c-125">Each image identifies a SQL Server version and an operating system.</span></span> 
6. <span data-ttu-id="51a9c-126">選取「Windows Server 2016 上的 SQL Server 2016 SP1 Developer」的映像。</span><span class="sxs-lookup"><span data-stu-id="51a9c-126">Select the image for SQL Server 2016 SP1 Developer on Windows Server 2016.</span></span>

   > [!TIP]
   > <span data-ttu-id="51a9c-127">本教學課程中使用 Developer 版本，因為它是免費供開發測試使用的 SQL Server 完整功能版。</span><span class="sxs-lookup"><span data-stu-id="51a9c-127">The Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes.</span></span> <span data-ttu-id="51a9c-128">您只需支付執行 VM 的費用。</span><span class="sxs-lookup"><span data-stu-id="51a9c-128">You pay only for the cost of running the VM.</span></span>

   > [!NOTE]
   > <span data-ttu-id="51a9c-129">SQL VM 映像在您所建立 VM 的每分鐘定價中包含 SQL Server 的授權成本 (Developer 和 Express 版本除外)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-129">SQL VM images include the licensing costs for SQL Server into the per-minute pricing of the VM you create (except for the Developer and Express editions).</span></span> <span data-ttu-id="51a9c-130">SQL Server Developer 免費供開發/測試 (非生產環境) 使用，SQL Express 免費供輕量型工作負載 (少於 1GB 記憶體、小於 10 GB 儲存體) 使用。</span><span class="sxs-lookup"><span data-stu-id="51a9c-130">SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1 GB memory, less than 10-GB storage).</span></span>
   > <span data-ttu-id="51a9c-131">另一個選項是自備授權 (BYOL)，並只針對 VM 付費。</span><span class="sxs-lookup"><span data-stu-id="51a9c-131">There is another option to bring-your-own-license (BYOL) and pay only for the VM.</span></span> <span data-ttu-id="51a9c-132">這些映像的名稱前面會有 {BYOL}。</span><span class="sxs-lookup"><span data-stu-id="51a9c-132">Those image names are prefixed with {BYOL}.</span></span> <span data-ttu-id="51a9c-133">如需這些選項的詳細資訊，請參閱 [SQL Server Azure VM 的定價指導方針](virtual-machines-windows-sql-server-pricing-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-133">For more information on these options, see [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

7. <span data-ttu-id="51a9c-134">在 [選取部署模型] 底下，確認已選取 [Resource Manager]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-134">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="51a9c-135">Resource Manager 是新的虛擬機器建議採用的部署模型。</span><span class="sxs-lookup"><span data-stu-id="51a9c-135">Resource Manager is the recommended deployment model for new virtual machines.</span></span> <span data-ttu-id="51a9c-136">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-136">Click **Create**.</span></span>

    ![使用 Resource Manager 建立 SQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-the-vm"></a><span data-ttu-id="51a9c-138">設定 VM</span><span class="sxs-lookup"><span data-stu-id="51a9c-138">Configure the VM</span></span>
<span data-ttu-id="51a9c-139">有五個刀鋒視窗可用來設定 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a9c-139">There are five blades for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="51a9c-140">步驟</span><span class="sxs-lookup"><span data-stu-id="51a9c-140">Step</span></span> | <span data-ttu-id="51a9c-141">說明</span><span class="sxs-lookup"><span data-stu-id="51a9c-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51a9c-142">**基本概念**</span><span class="sxs-lookup"><span data-stu-id="51a9c-142">**Basics**</span></span> |[<span data-ttu-id="51a9c-143">設定基本設定</span><span class="sxs-lookup"><span data-stu-id="51a9c-143">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="51a9c-144">**大小**</span><span class="sxs-lookup"><span data-stu-id="51a9c-144">**Size**</span></span> |[<span data-ttu-id="51a9c-145">選擇虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="51a9c-145">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="51a9c-146">**設定**</span><span class="sxs-lookup"><span data-stu-id="51a9c-146">**Settings**</span></span> |[<span data-ttu-id="51a9c-147">設定選用功能</span><span class="sxs-lookup"><span data-stu-id="51a9c-147">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="51a9c-148">**SQL Server 設定**</span><span class="sxs-lookup"><span data-stu-id="51a9c-148">**SQL Server settings**</span></span> |[<span data-ttu-id="51a9c-149">進行 SQL Server 設定</span><span class="sxs-lookup"><span data-stu-id="51a9c-149">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="51a9c-150">**摘要**</span><span class="sxs-lookup"><span data-stu-id="51a9c-150">**Summary**</span></span> |[<span data-ttu-id="51a9c-151">檢閱摘要</span><span class="sxs-lookup"><span data-stu-id="51a9c-151">Review the summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="51a9c-152">1.設定基本設定</span><span class="sxs-lookup"><span data-stu-id="51a9c-152">1. Configure basic settings</span></span>
<span data-ttu-id="51a9c-153">在 [基本概念]  刀鋒視窗中提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="51a9c-153">On the **Basics** blade, provide the following information:</span></span>

* <span data-ttu-id="51a9c-154">輸入唯一的虛擬機器 [名稱] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-154">Enter a unique virtual machine **Name**.</span></span>
* <span data-ttu-id="51a9c-155">指定 VM 上本機系統管理員帳戶的 [使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-155">Specify a **User name** for the local administrator account on the VM.</span></span> <span data-ttu-id="51a9c-156">這個帳戶也會加入至 SQL Server **sysadmin** 固定伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="51a9c-156">This account is also added to the SQL Server **sysadmin** fixed server role.</span></span>
* <span data-ttu-id="51a9c-157">提供強式 [密碼] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-157">Provide a strong **Password**.</span></span>
* <span data-ttu-id="51a9c-158">如果您有多個訂用帳戶，請確認訂用帳戶適用於新的 VM。</span><span class="sxs-lookup"><span data-stu-id="51a9c-158">If you have multiple subscriptions, verify that the subscription is correct for the new VM.</span></span>
* <span data-ttu-id="51a9c-159">在 [資源群組]  方塊中，輸入新資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="51a9c-159">In the **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="51a9c-160">或者，若要使用現有的資源群組，請按一下 [使用現有項目]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-160">Alternatively, to use an existing resource group click **Use existing**.</span></span> <span data-ttu-id="51a9c-161">資源群組是 Azure (虛擬機器、儲存體帳戶、虛擬網路等) 中相關資源的集合。</span><span class="sxs-lookup"><span data-stu-id="51a9c-161">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="51a9c-162">如果您只是測試或了解 Azure 中的 SQL Server 部署，使用新的資源群組很有幫助。</span><span class="sxs-lookup"><span data-stu-id="51a9c-162">Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure.</span></span> <span data-ttu-id="51a9c-163">完成測試之後，請刪除資源群組以自動刪除此 VM 以及與該資源群組相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="51a9c-163">After you finish with your test, delete the resource group to automatically delete the VM and all resources associated with that resource group.</span></span> <span data-ttu-id="51a9c-164">如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-164">For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).</span></span>
  > 
  > 
* <span data-ttu-id="51a9c-165">選取此部署的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="51a9c-165">Select a **Location** for this deployment.</span></span>
* <span data-ttu-id="51a9c-166">按一下 [確定]  來儲存設定。</span><span class="sxs-lookup"><span data-stu-id="51a9c-166">Click **OK** to save the settings.</span></span>
  
    ![SQL 基本概念刀鋒視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="51a9c-168">2.選擇虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="51a9c-168">2. Choose virtual machine size</span></span>
<span data-ttu-id="51a9c-169">在 [大小] 步驟上，請在 [選擇大小] 刀鋒視窗中選擇虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="51a9c-169">On the **Size** step, choose a virtual machine size in the **Choose a size** blade.</span></span> <span data-ttu-id="51a9c-170">此刀鋒視窗一開始會顯示以您選取的映像為基礎的建議機器大小。</span><span class="sxs-lookup"><span data-stu-id="51a9c-170">The blade initially displays recommended machine sizes based on the image you selected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51a9c-171">[選擇大小] 刀鋒視窗上顯示的估計每月成本不包含 SQL Server 授權成本。</span><span class="sxs-lookup"><span data-stu-id="51a9c-171">The estimated monthly cost displayed on the **Choose a size** blade does not include SQL Server licensing costs.</span></span> <span data-ttu-id="51a9c-172">這項預估每月成本就是 VM 單獨的成本。</span><span class="sxs-lookup"><span data-stu-id="51a9c-172">This estimated monthly cost is the cost of the VM alone.</span></span> <span data-ttu-id="51a9c-173">若為 SQL Server 的 Express 和 Developer 版本，這是預估的總成本。</span><span class="sxs-lookup"><span data-stu-id="51a9c-173">For the Express and Developer editions of SQL Server, this is the total estimated cost.</span></span> <span data-ttu-id="51a9c-174">若為其他版本，請參閱 [Windows 虛擬機器價格頁面](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)，然後選取您的目標 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="51a9c-174">For other editions, see the [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server.</span></span> <span data-ttu-id="51a9c-175">另請參閱 [SQL Server Azure VM 的定價指導方針](virtual-machines-windows-sql-server-pricing-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-175">Also see the [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

![SQL VM 大小選項](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="51a9c-177">針對生產工作負載，建議選取可支援 [進階儲存體](../../../storage/storage-premium-storage.md)的虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="51a9c-177">For production workloads, we recommend selecting a virtual machine size that supports [Premium Storage](../../../storage/storage-premium-storage.md).</span></span> <span data-ttu-id="51a9c-178">如果您不需要該層級的效能，請使用 [檢視全部]  按鈕來顯示所有機器大小選項。</span><span class="sxs-lookup"><span data-stu-id="51a9c-178">If you do not require that level of performance, use the **View all** button, which shows all machine size options.</span></span> <span data-ttu-id="51a9c-179">例如，您可能會將較小的機器使用開發或測試環境。</span><span class="sxs-lookup"><span data-stu-id="51a9c-179">For example, you might use a smaller machine size for a development or test environment.</span></span>

> [!NOTE]
> <span data-ttu-id="51a9c-180">如需關於虛擬機器大小的詳細資訊，請參閱[虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-180">For more information about virtual machine sizes, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="51a9c-181">如需有關 SQL Server VM 大小的考量，請參閱 [Azure 虛擬機器中的 SQL Server 效能最佳作法](virtual-machines-windows-sql-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-181">For considerations about SQL Server VM sizes, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

<span data-ttu-id="51a9c-182">選擇您的機器大小，然後按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-182">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="51a9c-183">3.設定選用功能</span><span class="sxs-lookup"><span data-stu-id="51a9c-183">3. Configure optional features</span></span>
<span data-ttu-id="51a9c-184">在 [設定]  刀鋒視窗上，設定虛擬機器的 Azure 儲存體、網路功能及監視功能。</span><span class="sxs-lookup"><span data-stu-id="51a9c-184">On the **Settings** blade, configure Azure storage, networking, and monitoring for the virtual machine.</span></span>

* <span data-ttu-id="51a9c-185">在 [儲存體] 底下，指定 [標準] 或 [進階 (SSD)] 的 [磁碟類型]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-185">Under **Storage**, specify a **Disk type** of either Standard or Premium (SSD).</span></span> <span data-ttu-id="51a9c-186">針對生產環境工作負載，建議使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="51a9c-186">Premium storage is recommended for production workloads.</span></span>

> [!NOTE]
> <span data-ttu-id="51a9c-187">如果您對不支援進階儲存體的機器大小選取 [進階 (SSD)]，您的機器大小會自動變更。</span><span class="sxs-lookup"><span data-stu-id="51a9c-187">If you select Premium (SSD) for a machine size that does not support Premium Storage, your machine size changes automatically.</span></span>  
> 
> 

* <span data-ttu-id="51a9c-188">在 [儲存體帳戶] 底下，您可以接受自動佈建的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="51a9c-188">Under **Storage account**, you can accept the automatically provisioned storage account name.</span></span> <span data-ttu-id="51a9c-189">您也可以按一下 [儲存體帳戶]  ，以選擇現有帳戶並設定儲存體帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="51a9c-189">You can also click on **Storage account** to choose an existing account and configure the storage account type.</span></span> <span data-ttu-id="51a9c-190">Azure 預設會建立具有本地備援儲存體的新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51a9c-190">By default, Azure creates a new storage account with locally redundant storage.</span></span> <span data-ttu-id="51a9c-191">如需儲存體選項的詳細資訊，請參閱 [Azure 儲存體複寫](../../../storage/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-191">For more information about storage options, see [Azure Storage replication](../../../storage/storage-redundancy.md).</span></span>
* <span data-ttu-id="51a9c-192">在 [網路] 底下，您可以接受自動填入的值。</span><span class="sxs-lookup"><span data-stu-id="51a9c-192">Under **Network**, you can accept the automatically populated values.</span></span> <span data-ttu-id="51a9c-193">也可以按一下每個功能，手動設定 [虛擬網路]、[子網路]、[公用 IP 位址] 及 [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-193">You can also click on each feature to manually configure the **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="51a9c-194">基於本教學課程的用途，您可以保留預設值。</span><span class="sxs-lookup"><span data-stu-id="51a9c-194">For the purposes of this tutorial, keep the default values.</span></span>
* <span data-ttu-id="51a9c-195">Azure 預設會使用為 VM 指定的相同儲存體帳戶來啟用 [監視]  。</span><span class="sxs-lookup"><span data-stu-id="51a9c-195">Azure enables **Monitoring** by default with the same storage account designated for the VM.</span></span> <span data-ttu-id="51a9c-196">您可以在這裡變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="51a9c-196">You can change these settings here.</span></span>
* <span data-ttu-id="51a9c-197">在 [可用性設定組] 底下，指定可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="51a9c-197">Under **Availability set**, specify an availability set.</span></span> <span data-ttu-id="51a9c-198">基於本教學課程的目的，您可以選取 [無] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-198">For the purposes of this tutorial, you can select **none**.</span></span> <span data-ttu-id="51a9c-199">如果您打算設定「SQL AlwaysOn 可用性群組」，請設定可用性以避免重新建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a9c-199">If you plan to set up SQL AlwaysOn Availability Groups, configure the availability to avoid recreating the virtual machine.</span></span>  <span data-ttu-id="51a9c-200">如需詳細資訊，請參閱 [管理虛擬機器的可用性](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-200">For more information, see [Manage the Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="51a9c-201">完成這些設定時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-201">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="51a9c-202">4.進行 SQL Server 設定</span><span class="sxs-lookup"><span data-stu-id="51a9c-202">4. Configure SQL server settings</span></span>
<span data-ttu-id="51a9c-203">在 [SQL Server 設定]  刀鋒視窗上，設定 SQL Server 的特定設定和最佳化。</span><span class="sxs-lookup"><span data-stu-id="51a9c-203">On the **SQL Server settings** blade, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="51a9c-204">您可以為 SQL Server 進行的設定包括下列設定。</span><span class="sxs-lookup"><span data-stu-id="51a9c-204">The settings that you can configure for SQL Server include the following settings.</span></span>

| <span data-ttu-id="51a9c-205">設定</span><span class="sxs-lookup"><span data-stu-id="51a9c-205">Setting</span></span> |
| --- |
| [<span data-ttu-id="51a9c-206">連線能力</span><span class="sxs-lookup"><span data-stu-id="51a9c-206">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="51a9c-207">驗證</span><span class="sxs-lookup"><span data-stu-id="51a9c-207">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="51a9c-208">儲存體組態</span><span class="sxs-lookup"><span data-stu-id="51a9c-208">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="51a9c-209">自動修補</span><span class="sxs-lookup"><span data-stu-id="51a9c-209">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="51a9c-210">自動備份</span><span class="sxs-lookup"><span data-stu-id="51a9c-210">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="51a9c-211">Azure 金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="51a9c-211">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="51a9c-212">R 服務</span><span class="sxs-lookup"><span data-stu-id="51a9c-212">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="51a9c-213">連線能力</span><span class="sxs-lookup"><span data-stu-id="51a9c-213">Connectivity</span></span>
<span data-ttu-id="51a9c-214">在 [SQL 連線] 底下，指定您要對此 VM 上的 SQL Server 執行個體進行的存取類型。</span><span class="sxs-lookup"><span data-stu-id="51a9c-214">Under **SQL connectivity**, specify the type of access you want to the SQL Server instance on this VM.</span></span> <span data-ttu-id="51a9c-215">基於本教學課程的目的，指定 [公用 (網際網路)]  以允許從網際網路上的電腦或服務連線到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="51a9c-215">For the purposes of this tutorial, select **Public (internet)** to allow connections to SQL Server from machines or services on the internet.</span></span> <span data-ttu-id="51a9c-216">在已選取此選項的情況下，Azure 會自動設定防火牆和網路安全性群組以允許連接埠 1433 上的流量。</span><span class="sxs-lookup"><span data-stu-id="51a9c-216">With this option selected, Azure automatically configures the firewall and the network security group to allow traffic on port 1433.</span></span>  

![SQL 連線選項](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

<span data-ttu-id="51a9c-218">若要透過網際網路連接到 SQL Server，您也必須啟用下一節所述的「SQL Server 驗證」。</span><span class="sxs-lookup"><span data-stu-id="51a9c-218">To connect to SQL Server via the internet, you also must enable SQL Server Authentication, which is described in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="51a9c-219">很可能對您的 SQL Server VM 的網路通訊帶來更多限制。</span><span class="sxs-lookup"><span data-stu-id="51a9c-219">It is possible to add more restrictions for the network communications to your SQL Server VM.</span></span> <span data-ttu-id="51a9c-220">建立 VM 後，您可以編輯網路安全性群組以新增更多限制。</span><span class="sxs-lookup"><span data-stu-id="51a9c-220">You can add more restrictions by editing the Network Security Group after the VM is created.</span></span> <span data-ttu-id="51a9c-221">如需詳細資訊，請參閱 [什麼是網路安全性群組 (NSG)？](../../../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="51a9c-221">For more information, see [What is a Network Security Group (NSG)?](../../../virtual-network/virtual-networks-nsg.md)</span></span>
> 
> 

<span data-ttu-id="51a9c-222">如果您偏好不要啟用透過網際網路連線到 Database Engine 的功能，請選擇下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="51a9c-222">If you would prefer to not enable connections to the Database Engine via the internet, choose one of the following options:</span></span>

* <span data-ttu-id="51a9c-223"> 只允許從 VM 內連接到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="51a9c-223">**Local (inside VM only)** to allow connections to SQL Server only from within the VM.</span></span>
* <span data-ttu-id="51a9c-224"> 允許從相同虛擬網路中的電腦或服務連接到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="51a9c-224">**Private (within Virtual Network)** to allow connections to SQL Server from machines or services in the same virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="51a9c-225">SQL Server Express 版本的虛擬機器映像不會自動啟用 TCP/IP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="51a9c-225">The virtual machine image for SQL Server Express edition does not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="51a9c-226">這也適用於公用和私用連線能力選項。</span><span class="sxs-lookup"><span data-stu-id="51a9c-226">This is true even for the Public and  Private connectivity options.</span></span> <span data-ttu-id="51a9c-227">在 Express 版本中，您必須在建立 VM 之後，使用「SQL Server 組態管理員」來 [手動啟用 TCP/IP 通訊協定](#configure-sql-server-to-listen-on-the-tcp-protocol) 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-227">For Express edition, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating the VM.</span></span>
> 
> 

<span data-ttu-id="51a9c-228">一般情況下，選擇您的案例允許的最嚴格連線能力，即可改善安全性。</span><span class="sxs-lookup"><span data-stu-id="51a9c-228">In general, improve security by choosing the most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="51a9c-229">但所有透過網路安全性群組規則和 SQL/Windows 驗證的選項都是安全的。</span><span class="sxs-lookup"><span data-stu-id="51a9c-229">But all the options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span>

<span data-ttu-id="51a9c-230"> 預設為 1433。</span><span class="sxs-lookup"><span data-stu-id="51a9c-230">**Port** defaults to 1433.</span></span> <span data-ttu-id="51a9c-231">您可以指定其他連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="51a9c-231">You can specify a different port number.</span></span>
<span data-ttu-id="51a9c-232">如需詳細資訊，請參閱 [連接到 SQL Server 虛擬機器 (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-232">For more information, see [Connect to a SQL Server Virtual Machine (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md).</span></span>

### <a name="authentication"></a><span data-ttu-id="51a9c-233">驗證</span><span class="sxs-lookup"><span data-stu-id="51a9c-233">Authentication</span></span>
<span data-ttu-id="51a9c-234">如果您需要「SQL Server 驗證」，請按一下 [SQL 驗證]  under 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-234">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![SQL Server 驗證](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> <span data-ttu-id="51a9c-236">如果您打算透過網際網路存取 SQL Server (也就是 [公用] 連線選項)，您必須在這裡啟用 SQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="51a9c-236">If you plan to access SQL Server over the internet (that is, the Public connectivity option), you must enable SQL authentication here.</span></span> <span data-ttu-id="51a9c-237">對 SQL Server 進行公用存取需要使用「SQL 驗證」。</span><span class="sxs-lookup"><span data-stu-id="51a9c-237">Public access to the SQL Server requires the use of SQL Authentication.</span></span>
> 
> 

<span data-ttu-id="51a9c-238">如果您啟用 [SQL Server 驗證]，請指定 [登入名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-238">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="51a9c-239">這個使用者名稱會設定為 SQL Server 驗證登入以及 **sysadmin** 固定伺服器角色的成員。</span><span class="sxs-lookup"><span data-stu-id="51a9c-239">This user name is configured as a SQL Server Authentication login and member of the **sysadmin** fixed server role.</span></span> <span data-ttu-id="51a9c-240">如需驗證模式的詳細資訊，請參閱[選擇驗證模式](http://msdn.microsoft.com/library/ms144284.aspx)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-240">For more information about Authentication Modes, see [Choose an Authentication Mode](http://msdn.microsoft.com/library/ms144284.aspx).</span></span>

<span data-ttu-id="51a9c-241">如果您未啟用 SQL Server 驗證，您可以在 VM 上使用本機系統管理員帳戶連接到 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51a9c-241">If you do not enable SQL Server Authentication, then you can use the local Administrator account on the VM to connect to the SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="51a9c-242">儲存體組態</span><span class="sxs-lookup"><span data-stu-id="51a9c-242">Storage configuration</span></span>
<span data-ttu-id="51a9c-243">按一下 [儲存體組態]  以指定儲存體需求。</span><span class="sxs-lookup"><span data-stu-id="51a9c-243">Click **Storage configuration** to specify the storage requirements.</span></span>

![SQL 儲存體組態](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> <span data-ttu-id="51a9c-245">如果您選取 [標準] 儲存體，則無法使用此選項。</span><span class="sxs-lookup"><span data-stu-id="51a9c-245">If you select Standard storage, this option is not available.</span></span> <span data-ttu-id="51a9c-246">自動儲存體最佳化只適用於進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="51a9c-246">Automatic storage optimization is available only for Premium Storage.</span></span>
> 
> 

<span data-ttu-id="51a9c-247">您可以用每秒輸入/輸出作業數 (IOPs)、輸送量 (單位為 MB/s) 及總儲存體大小來指定需求。</span><span class="sxs-lookup"><span data-stu-id="51a9c-247">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="51a9c-248">請使用滑動標尺來設定這些值。</span><span class="sxs-lookup"><span data-stu-id="51a9c-248">Configure these values by using the sliding scales.</span></span> <span data-ttu-id="51a9c-249">入口網站會自動根據這些需求計算磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="51a9c-249">The portal automatically calculates the number of disks based on these requirements.</span></span>

<span data-ttu-id="51a9c-250">Azure 預設會針對 5000 IOPs、200 MBs 及 1 TB 的儲存體空間進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="51a9c-250">By default, Azure optimizes the storage for 5000 IOPs, 200 MBs, and 1 TB of storage space.</span></span> <span data-ttu-id="51a9c-251">您可以根據工作負載變更這些儲存體設定。</span><span class="sxs-lookup"><span data-stu-id="51a9c-251">You can change these storage settings based on workload.</span></span> <span data-ttu-id="51a9c-252">在 [儲存體最佳化] 底下，選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="51a9c-252">Under **Storage optimized for**, select one of the following options:</span></span>

* <span data-ttu-id="51a9c-253"> 是預設設定，支援大多數工作負載。</span><span class="sxs-lookup"><span data-stu-id="51a9c-253">**General** is the default setting and supports most workloads.</span></span>
* <span data-ttu-id="51a9c-254"> 可將儲存體最佳化來處理傳統資料庫 OLTP 工作負載。</span><span class="sxs-lookup"><span data-stu-id="51a9c-254">**Transactional** processing optimizes the storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="51a9c-255"> 可將儲存體最佳化來處理分析和報告工作負載。</span><span class="sxs-lookup"><span data-stu-id="51a9c-255">**Data warehousing** optimizes the storage for analytic and reporting workloads.</span></span>

> [!NOTE]
> <span data-ttu-id="51a9c-256">滑桿上的上限視您選取的虛擬機器大小而有所不同。</span><span class="sxs-lookup"><span data-stu-id="51a9c-256">The upper limits on the sliders vary depending on your selected virtual machine size.</span></span>
> 
> 

### <a name="automated-patching"></a><span data-ttu-id="51a9c-257">自動修補</span><span class="sxs-lookup"><span data-stu-id="51a9c-257">Automated patching</span></span>
<span data-ttu-id="51a9c-258">**Automated patching** 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-258">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="51a9c-259">自動修補可讓 Azure 自動修補 SQL Server 和作業系統。</span><span class="sxs-lookup"><span data-stu-id="51a9c-259">Automated patching allows Azure to automatically patch SQL Server and the operating system.</span></span> <span data-ttu-id="51a9c-260">請為維護期間指定一週當中的某一天、時間及持續時間。</span><span class="sxs-lookup"><span data-stu-id="51a9c-260">Specify a day of the week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="51a9c-261">Azure 會在此維護期間執行修補。</span><span class="sxs-lookup"><span data-stu-id="51a9c-261">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="51a9c-262">維護期間排程會使用 VM 地區設定做為時間。</span><span class="sxs-lookup"><span data-stu-id="51a9c-262">The maintenance window schedule uses the VM locale for time.</span></span> <span data-ttu-id="51a9c-263">如果您不想要讓 Azure 自動修補 SQL Server 和作業系統，請按一下 [停用] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-263">If you do not want Azure to automatically patch SQL Server and the operating system, click **Disable**.</span></span>  

![SQL 自動修補](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="51a9c-265">如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補](virtual-machines-windows-sql-automated-patching.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-265">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="51a9c-266">自動備份</span><span class="sxs-lookup"><span data-stu-id="51a9c-266">Automated backup</span></span>
<span data-ttu-id="51a9c-267">在 [自動備份] 底下，可以為所有資料庫啟用自動資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="51a9c-267">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="51a9c-268">預設會停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="51a9c-268">Automated backup is disabled by default.</span></span>

<span data-ttu-id="51a9c-269">當您啟用 SQL 自動備份時，您可以進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="51a9c-269">When you enable SQL automated backup, you can configure the following settings:</span></span>

* <span data-ttu-id="51a9c-270">備份的保留期限 (天數)</span><span class="sxs-lookup"><span data-stu-id="51a9c-270">Retention period (days) for backups</span></span>
* <span data-ttu-id="51a9c-271">要用於備份的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="51a9c-271">Storage account to use for backups</span></span>
* <span data-ttu-id="51a9c-272">備份的加密選項和密碼</span><span class="sxs-lookup"><span data-stu-id="51a9c-272">Encryption option and password for backups</span></span>
* <span data-ttu-id="51a9c-273">備份系統資料庫</span><span class="sxs-lookup"><span data-stu-id="51a9c-273">Backup system databases</span></span>
* <span data-ttu-id="51a9c-274">設定備份排程</span><span class="sxs-lookup"><span data-stu-id="51a9c-274">Configure backup schedule</span></span>

<span data-ttu-id="51a9c-275">若要加密備份，請按一下 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-275">To encrypt the backup, click **Enable**.</span></span> <span data-ttu-id="51a9c-276">然後指定 [密碼] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-276">Then specify the **Password**.</span></span> <span data-ttu-id="51a9c-277">Azure 會建立憑證來加密備份，並使用指定的密碼來保護該憑證。</span><span class="sxs-lookup"><span data-stu-id="51a9c-277">Azure creates a certificate to encrypt the backups and uses the specified password to protect that certificate.</span></span>

![SQL 自動備份](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="51a9c-279">如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的自動化備份](virtual-machines-windows-sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-279">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="51a9c-280">Azure 金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="51a9c-280">Azure Key Vault integration</span></span>
<span data-ttu-id="51a9c-281">若要在 Azure 中儲存用於加密的安全性密碼，請按一下 [Azure 金鑰保存庫整合]，然後按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-281">To store security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure 金鑰保存庫整合](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="51a9c-283">下表列出設定「Azure 金鑰保存庫整合」時所需的參數。</span><span class="sxs-lookup"><span data-stu-id="51a9c-283">The following table lists the parameters required to configure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="51a9c-284">參數</span><span class="sxs-lookup"><span data-stu-id="51a9c-284">PARAMETER</span></span> | <span data-ttu-id="51a9c-285">說明</span><span class="sxs-lookup"><span data-stu-id="51a9c-285">DESCRIPTION</span></span> | <span data-ttu-id="51a9c-286">範例</span><span class="sxs-lookup"><span data-stu-id="51a9c-286">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51a9c-287">**金鑰保存庫 URL**</span><span class="sxs-lookup"><span data-stu-id="51a9c-287">**Key Vault URL**</span></span> |<span data-ttu-id="51a9c-288">金鑰保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="51a9c-288">The location of the key vault.</span></span> |<span data-ttu-id="51a9c-289">https://contosokeyvault.vault.azure.net/</span><span class="sxs-lookup"><span data-stu-id="51a9c-289">https://contosokeyvault.vault.azure.net/</span></span> |
| <span data-ttu-id="51a9c-290">**主體名稱**</span><span class="sxs-lookup"><span data-stu-id="51a9c-290">**Principal name**</span></span> |<span data-ttu-id="51a9c-291">Azure Active Directory 服務主體名稱。</span><span class="sxs-lookup"><span data-stu-id="51a9c-291">Azure Active Directory service principal name.</span></span> <span data-ttu-id="51a9c-292">此名稱也稱為「用戶端識別碼」。</span><span class="sxs-lookup"><span data-stu-id="51a9c-292">This name is also referred to as the Client ID.</span></span> |<span data-ttu-id="51a9c-293">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="51a9c-293">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="51a9c-294">**主體密碼**</span><span class="sxs-lookup"><span data-stu-id="51a9c-294">**Principal secret**</span></span> |<span data-ttu-id="51a9c-295">Azure Active Directory 服務主體密碼。</span><span class="sxs-lookup"><span data-stu-id="51a9c-295">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="51a9c-296">此密碼也稱為「用戶端密碼」。</span><span class="sxs-lookup"><span data-stu-id="51a9c-296">This secret is also referred to as the Client Secret.</span></span> |<span data-ttu-id="51a9c-297">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="51a9c-297">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="51a9c-298">**認證名稱**</span><span class="sxs-lookup"><span data-stu-id="51a9c-298">**Credential name**</span></span> |<span data-ttu-id="51a9c-299">**認證名稱**：AKV 整合會在 SQL Server 內建立認證，允許 VM 具有金鑰保存庫的存取權。</span><span class="sxs-lookup"><span data-stu-id="51a9c-299">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span></span> <span data-ttu-id="51a9c-300">選擇此認證的名稱。</span><span class="sxs-lookup"><span data-stu-id="51a9c-300">Choose a name for this credential.</span></span> |<span data-ttu-id="51a9c-301">mycred1</span><span class="sxs-lookup"><span data-stu-id="51a9c-301">mycred1</span></span> |

<span data-ttu-id="51a9c-302">如需詳細資訊，請參閱 [在 Azure VM 上設定 SQL Server 的 Azure 金鑰保存庫整合](virtual-machines-windows-ps-sql-keyvault.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-302">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

<span data-ttu-id="51a9c-303">完成 SQL Server 設定之後，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="51a9c-303">When you are finished configuring SQL Server settings, click **OK**.</span></span>

### <a name="r-services"></a><span data-ttu-id="51a9c-304">R 服務</span><span class="sxs-lookup"><span data-stu-id="51a9c-304">R services</span></span>
<span data-ttu-id="51a9c-305">您可以啟用 [SQL Server R 服務](https://msdn.microsoft.com/library/mt604845.aspx)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-305">You can enable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="51a9c-306">SQL Server R 服務可讓您搭配 SQL Server 2016 使用進階分析。</span><span class="sxs-lookup"><span data-stu-id="51a9c-306">SQL Server R Services enables you to use advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="51a9c-307">按一下 [建立]  on the **SQL Server Settings** 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="51a9c-307">Click **Enable** on the **SQL Server Settings** blade.</span></span>

![啟用 SQL Server R 服務](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-the-summary"></a><span data-ttu-id="51a9c-309">5.檢閱摘要</span><span class="sxs-lookup"><span data-stu-id="51a9c-309">5. Review the summary</span></span>
<span data-ttu-id="51a9c-310">在 [摘要] 刀鋒視窗上檢閱摘要，然後按一下 [確定] 來建立為此 VM 指定的 SQL Server、資源群組及資源。</span><span class="sxs-lookup"><span data-stu-id="51a9c-310">On the **Summary** blade, review the summary and click **OK** to create SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="51a9c-311">您可以從 Azure 入口網站監視部署。</span><span class="sxs-lookup"><span data-stu-id="51a9c-311">You can monitor the deployment from the azure portal.</span></span> <span data-ttu-id="51a9c-312">畫面頂端的 [通知]  按鈕會顯示基本的部署狀態。</span><span class="sxs-lookup"><span data-stu-id="51a9c-312">The **Notifications** button at the top of the screen shows basic status of the deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="51a9c-313">為了讓您了解部署時間，我已使用預設設定將 SQL VM 部署到美國東部區域。</span><span class="sxs-lookup"><span data-stu-id="51a9c-313">To provide you with an idea on deployment times, I deployed a SQL VM to the East US region with default settings.</span></span> <span data-ttu-id="51a9c-314">此測試部署總共花了 26 分鐘才完成。</span><span class="sxs-lookup"><span data-stu-id="51a9c-314">This test deployment took a total of 26 minutes to complete.</span></span> <span data-ttu-id="51a9c-315">但是根據您的區域和選取的設定，您可能會經歷較快或較慢的部署時間。</span><span class="sxs-lookup"><span data-stu-id="51a9c-315">But you might experience a faster or slower deployment time based on your region and selected settings.</span></span>
> 
> 

## <a name="open-the-vm-with-remote-desktop"></a><span data-ttu-id="51a9c-316">透過遠端桌面開啟 VM</span><span class="sxs-lookup"><span data-stu-id="51a9c-316">Open the VM with Remote Desktop</span></span>
<span data-ttu-id="51a9c-317">使用下列步驟，透過遠端桌面連接到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a9c-317">Use the following steps to connect to the virtual machine with Remote Desktop:</span></span>

1. <span data-ttu-id="51a9c-318">建置 Azure VM 之後，VM 的圖示會出現在 Azure 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="51a9c-318">After the Azure VM is built, the icon for the VM appears on your Azure dashboard.</span></span> <span data-ttu-id="51a9c-319">瀏覽現有的虛擬機器，也可以找到它。</span><span class="sxs-lookup"><span data-stu-id="51a9c-319">You can also find it by browsing your existing virtual machines.</span></span> <span data-ttu-id="51a9c-320">按一下新的 SQL 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a9c-320">Click on your new SQL virtual machine.</span></span> <span data-ttu-id="51a9c-321">[虛擬機器]  刀鋒視窗會顯示您的虛擬機器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="51a9c-321">A **Virtual machine** blade displays your virtual machine details.</span></span>
2. <span data-ttu-id="51a9c-322">在 [虛擬機器] 刀鋒視窗頂端，按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-322">At the top of the **Virtual machine** blade, click **Connect**.</span></span>
3. <span data-ttu-id="51a9c-323">瀏覽器會為 VM 下載 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="51a9c-323">The browser downloads an RDP file for the VM.</span></span> <span data-ttu-id="51a9c-324">開啟 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="51a9c-324">Open the RDP file.</span></span>
    <span data-ttu-id="51a9c-325">![SQL VM 的遠端桌面](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span><span class="sxs-lookup"><span data-stu-id="51a9c-325">![Remote Desktop to SQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span></span>
4. <span data-ttu-id="51a9c-326">[遠端桌面連線] 會通知您無法識別這個遠端連線的發行者。</span><span class="sxs-lookup"><span data-stu-id="51a9c-326">The Remote Desktop Connection notifies you that the publisher of this remote connection cannot be identified.</span></span> <span data-ttu-id="51a9c-327">按一下 [連接]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="51a9c-327">Click **Connect** to continue.</span></span>
5. <span data-ttu-id="51a9c-328">在 [Windows 安全性] 對話方塊中按一下 [使用其他帳戶]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-328">In the **Windows Security** dialog, click **Use another account**.</span></span>
6. <span data-ttu-id="51a9c-329">針對 [使用者名稱]，輸入**\<使用者名稱>**，其中 <user name> 是您設定 VM 時所指定的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="51a9c-329">For **User name** type **\<user name>**, where <user name> is the user name that you specified when you configured the VM.</span></span> <span data-ttu-id="51a9c-330">您必須在名稱前面加入初始反斜線。</span><span class="sxs-lookup"><span data-stu-id="51a9c-330">You have to add an initial backslash before the name.</span></span>
7. <span data-ttu-id="51a9c-331">輸入您先前為此 VM 設定的 [密碼]，然後按一下 [確定] 進行連線。</span><span class="sxs-lookup"><span data-stu-id="51a9c-331">Type the **Password** that you previously configured for this VM, and then click **OK** to connect.</span></span>
8. <span data-ttu-id="51a9c-332">如果另一個 [遠端桌面連線] 對話方塊詢問您是否要連線，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-332">If another **Remote Desktop Connection** dialog asks you whether to connect, click **Yes**.</span></span>

<span data-ttu-id="51a9c-333">連線到 SQL Server 虛擬機器之後，您可以啟動 SQL Server Management Studio，然後使用您的本機系統管理員認證透過「Windows 驗證」進行連線。</span><span class="sxs-lookup"><span data-stu-id="51a9c-333">After you connect to the SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="51a9c-334">如果您已啟用 SQL Server 驗證，您也可以使用您在佈建期間所設定的 SQL 登入和密碼以 SQL 驗證連線。</span><span class="sxs-lookup"><span data-stu-id="51a9c-334">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using the SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="51a9c-335">存取電腦可讓您根據您的需求直接變更電腦和 SQL Server 設定。</span><span class="sxs-lookup"><span data-stu-id="51a9c-335">Access to the machine enables you to directly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="51a9c-336">例如，您可以設定防火牆設定或變更 SQL Server 組態設定。</span><span class="sxs-lookup"><span data-stu-id="51a9c-336">For example, you could configure the firewall settings or change SQL Server configuration settings.</span></span>

## <a name="connect-to-sql-server-remotely"></a><span data-ttu-id="51a9c-337">從遠端連接到 SQL Server</span><span class="sxs-lookup"><span data-stu-id="51a9c-337">Connect to SQL Server remotely</span></span>
<span data-ttu-id="51a9c-338">本教學課程中，我們選取了虛擬機器的 [公用] 存取權和 [SQL Server 驗證]。</span><span class="sxs-lookup"><span data-stu-id="51a9c-338">In this tutorial, we selected **Public** access for the virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="51a9c-339">這些設定會自動設定虛擬機器，以允許透過網際網路來自任何用戶端的 SQL Server 連線 (假設它們有正確的 SQL 登入)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-339">These settings automatically configured the virtual machine to allow SQL Server connections from any client over the internet (assuming they have the correct SQL login).</span></span>

> [!NOTE]
> <span data-ttu-id="51a9c-340">如果在佈建時您沒有選取 [公用]，則還必須執行其他步驟，才能透過網際網路存取您的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51a9c-340">If you did not select Public during provisioning, then extra steps are required to access your SQL Server instance over the internet.</span></span> <span data-ttu-id="51a9c-341">如需詳細資訊，請參閱[連接到 SQL Server 虛擬機器](virtual-machines-windows-sql-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-341">For more information, see  [Connect to a SQL Server Virtual Machine](virtual-machines-windows-sql-connect.md).</span></span>
> 
> 

<span data-ttu-id="51a9c-342">下列各節說明如何透過網際網路，從不同的電腦連接到您的 VM 上的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="51a9c-342">The following sections show how to connect to your SQL Server instance on your VM from a different computer over the internet.</span></span>

> [!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="51a9c-343">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51a9c-343">Next Steps</span></span>
<span data-ttu-id="51a9c-344">如需在 Azure 中使用 SQL Server 的其他資訊，請參閱 [Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 和[常見問題集](virtual-machines-windows-sql-server-iaas-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-344">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and the [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>

<span data-ttu-id="51a9c-345">如需 Azure 虛擬機器上 SQL Server 的影片概觀，請觀看 [Azure VM is the best platform for SQL Server 2016 (Azure VM 是 SQL Server 2016 的最佳平台)](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)。</span><span class="sxs-lookup"><span data-stu-id="51a9c-345">For a video overview of SQL Server on Azure Virtual Machines, watch [Azure VM is the best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).</span></span>

<span data-ttu-id="51a9c-346">[探索學習路徑](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) ：Azure 虛擬機器上的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="51a9c-346">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span>

