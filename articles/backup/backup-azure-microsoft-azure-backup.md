---
title: "使用 Azure 備份伺服器，將工作負載備份至 Azure | Microsoft Docs"
description: "使用 Azure 備份伺服器來保護工作負載，或備份至 Azure 入口網站。"
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: "Azure 備份伺服器; 保護工作負載; 備份工作負載"
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: c54468d71e0b383916e49847576a98303d659d38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="preparing-to-back-up-workloads-using-azure-backup-server"></a><span data-ttu-id="6de29-104">準備使用 Azure 備份伺服器來備份工作負載</span><span class="sxs-lookup"><span data-stu-id="6de29-104">Preparing to back up workloads using Azure Backup Server</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6de29-105">Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="6de29-105">Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
> * [<span data-ttu-id="6de29-106">SCDPM</span><span class="sxs-lookup"><span data-stu-id="6de29-106">SCDPM</span></span>](backup-azure-dpm-introduction.md)
>
>

<span data-ttu-id="6de29-107">本文說明如何準備環境，以使用 Azure 備份伺服器來備份工作負載。</span><span class="sxs-lookup"><span data-stu-id="6de29-107">This article explains how to prepare your environment to back up workloads using Azure Backup Server.</span></span> <span data-ttu-id="6de29-108">透過 Azure 備份伺服器，您將可從單一主控台保護 Hyper-V VM、Microsoft SQL Server、SharePoint Server、Microsoft Exchange 和 Windows 用戶端等應用程式工作負載。</span><span class="sxs-lookup"><span data-stu-id="6de29-108">With Azure Backup Server, you can protect application workloads such as Hyper-V VMs, Microsoft SQL Server, SharePoint Server, Microsoft Exchange, and Windows clients from a single console.</span></span>

> [!NOTE]
> <span data-ttu-id="6de29-109">Azure 備份伺服器現在可以保護 VMware VM，並提供改善的安全性功能。</span><span class="sxs-lookup"><span data-stu-id="6de29-109">Azure Backup Server can now protect VMware VMs and provides improved security capabilities.</span></span> <span data-ttu-id="6de29-110">依下列各節所述安裝此產品，並套用 Update 1 和最新的 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="6de29-110">Install the product as explained in the sections below; apply Update 1 and the latest Azure Backup Agent.</span></span> <span data-ttu-id="6de29-111">若要深入了解使用 Azure 備份伺服器備份 VMware 伺服器，請參閱文件：[使用 Azure 備份伺服器備份 VMware 伺服器](backup-azure-backup-server-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="6de29-111">To learn more about backing up VMware servers with Azure Backup Server, see the article, [Use Azure Backup Server to back up a VMware server](backup-azure-backup-server-vmware.md).</span></span> <span data-ttu-id="6de29-112">若要深入了解安全性功能，請參閱 [Azure 備份安全性功能文件](backup-azure-security-feature.md)。</span><span class="sxs-lookup"><span data-stu-id="6de29-112">To learn about security capabilities, refer to [Azure backup security features documentation](backup-azure-security-feature.md).</span></span>
>
>

<span data-ttu-id="6de29-113">您也可以保護基礎結構即服務 (IaaS) 工作負載，例如 Azure 中的 VM。</span><span class="sxs-lookup"><span data-stu-id="6de29-113">You can also protect Infrastructure as a Service (IaaS) workloads such as VMs in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6de29-114">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6de29-114">Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6de29-115">本文提供的資訊和程序可供還原使用 Resource Manager 模型部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="6de29-115">This article provides the information and procedures for restoring VMs deployed using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="6de29-116">Azure 備份伺服器承襲了 Data Protection Manager (DPM) 的大部分工作負載備份功能。</span><span class="sxs-lookup"><span data-stu-id="6de29-116">Azure Backup Server inherits much of the workload backup functionality from Data Protection Manager (DPM).</span></span> <span data-ttu-id="6de29-117">本文會連結至 DPM 文件，以說明其中的部分共用功能。</span><span class="sxs-lookup"><span data-stu-id="6de29-117">This article links to DPM documentation to explain some of the shared functionality.</span></span> <span data-ttu-id="6de29-118">雖然 Azure 備份伺服器共用許多與 DPM 相同的功能。</span><span class="sxs-lookup"><span data-stu-id="6de29-118">Though Azure Backup Server shares much of the same functionality as DPM.</span></span> <span data-ttu-id="6de29-119">Azure 備份伺服器並不會備份到磁帶，也無法與 System Center 整合。</span><span class="sxs-lookup"><span data-stu-id="6de29-119">Azure Backup Server does not back up to tape, nor does it integrate with System Center.</span></span>

## <a name="1-choose-an-installation-platform"></a><span data-ttu-id="6de29-120">1.選擇安裝平台</span><span class="sxs-lookup"><span data-stu-id="6de29-120">1. Choose an installation platform</span></span>
<span data-ttu-id="6de29-121">要啟動並執行 Azure 備份伺服器，第一個步驟是設定 Windows Server。</span><span class="sxs-lookup"><span data-stu-id="6de29-121">The first step towards getting the Azure Backup Server up and running is to set up a Windows Server.</span></span> <span data-ttu-id="6de29-122">伺服器可以位於 Azure 或內部部署中。</span><span class="sxs-lookup"><span data-stu-id="6de29-122">Your server can be in Azure or on-premises.</span></span>

### <a name="using-a-server-in-azure"></a><span data-ttu-id="6de29-123">使用 Azure 中的伺服器</span><span class="sxs-lookup"><span data-stu-id="6de29-123">Using a server in Azure</span></span>
<span data-ttu-id="6de29-124">在選擇用來執行 Azure 備份伺服器的伺服器時，建議您從 Windows Server 2012 R2 Datacenter 的資源庫映像來開始。</span><span class="sxs-lookup"><span data-stu-id="6de29-124">When choosing a server for running Azure Backup Server, it is recommended you start with a gallery image of Windows Server 2012 R2 Datacenter.</span></span> <span data-ttu-id="6de29-125">即使您之前從未使用過 Azure， [在 Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)一文會提供教學課程讓您在 Azure 中開始使用建議的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6de29-125">The article, [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), provides a tutorial for getting started with the recommended virtual machine in Azure, even if you've never used Azure before.</span></span> <span data-ttu-id="6de29-126">伺服器虛擬機器 (VM) 的最低建議需求應該是︰A2 標準，具備雙核心及 3.5 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="6de29-126">The recommended minimum requirements for the server virtual machine (VM) should be: A2 Standard with two cores and 3.5 GB RAM.</span></span>

<span data-ttu-id="6de29-127">使用 Azure 備份伺服器保護工作負載有許多細節需要注意。</span><span class="sxs-lookup"><span data-stu-id="6de29-127">Protecting workloads with Azure Backup Server has many nuances.</span></span> <span data-ttu-id="6de29-128">[將 DPM 安裝為 Azure 虛擬機器](https://technet.microsoft.com/library/jj852163.aspx)一文可協助說明這些細節。</span><span class="sxs-lookup"><span data-stu-id="6de29-128">The article, [Install DPM as an Azure virtual machine](https://technet.microsoft.com/library/jj852163.aspx), helps explain these nuances.</span></span> <span data-ttu-id="6de29-129">在部署機器之前，請先確實閱讀此文章。</span><span class="sxs-lookup"><span data-stu-id="6de29-129">Before deploying the machine, read this article completely.</span></span>

### <a name="using-an-on-premises-server"></a><span data-ttu-id="6de29-130">使用內部部署伺服器</span><span class="sxs-lookup"><span data-stu-id="6de29-130">Using an on-premises server</span></span>
<span data-ttu-id="6de29-131">若不想在 Azure 中執行基本伺服器，您可以在 Hyper-V VM、VMware VM 或實體主機上執行伺服器。</span><span class="sxs-lookup"><span data-stu-id="6de29-131">If you do not want to run the base server in Azure, you can run the server on a Hyper-V VM, a VMware VM, or a physical host.</span></span> <span data-ttu-id="6de29-132">伺服器硬體的最低建議需求是雙核心與 4 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="6de29-132">The recommended minimum requirements for the server hardware are two cores and 4 GB RAM.</span></span> <span data-ttu-id="6de29-133">下表列出支援的作業系統：</span><span class="sxs-lookup"><span data-stu-id="6de29-133">The supported operating systems are listed in the following table:</span></span>

| <span data-ttu-id="6de29-134">作業系統</span><span class="sxs-lookup"><span data-stu-id="6de29-134">Operating System</span></span> | <span data-ttu-id="6de29-135">平台</span><span class="sxs-lookup"><span data-stu-id="6de29-135">Platform</span></span> | <span data-ttu-id="6de29-136">SKU</span><span class="sxs-lookup"><span data-stu-id="6de29-136">SKU</span></span> |
|:--- | --- |:--- |
| <span data-ttu-id="6de29-137">Windows Server 2012 R2 和最新的 SP</span><span class="sxs-lookup"><span data-stu-id="6de29-137">Windows Server 2012 R2 and latest SPs</span></span> |<span data-ttu-id="6de29-138">64 位元</span><span class="sxs-lookup"><span data-stu-id="6de29-138">64 bit</span></span> |<span data-ttu-id="6de29-139">Standard、Datacenter、Foundation</span><span class="sxs-lookup"><span data-stu-id="6de29-139">Standard, Datacenter, Foundation</span></span> |
| <span data-ttu-id="6de29-140">Windows Server 2012 和最新的 SP</span><span class="sxs-lookup"><span data-stu-id="6de29-140">Windows Server 2012 and latest SPs</span></span> |<span data-ttu-id="6de29-141">64 位元</span><span class="sxs-lookup"><span data-stu-id="6de29-141">64 bit</span></span> |<span data-ttu-id="6de29-142">Datacenter、Foundation、Standard</span><span class="sxs-lookup"><span data-stu-id="6de29-142">Datacenter, Foundation, Standard</span></span> |
| <span data-ttu-id="6de29-143">Windows Storage Server 2012 R2 和最新的 SP</span><span class="sxs-lookup"><span data-stu-id="6de29-143">Windows Storage Server 2012 R2 and latest SPs</span></span> |<span data-ttu-id="6de29-144">64 位元</span><span class="sxs-lookup"><span data-stu-id="6de29-144">64 bit</span></span> |<span data-ttu-id="6de29-145">Standard、Workgroup</span><span class="sxs-lookup"><span data-stu-id="6de29-145">Standard, Workgroup</span></span> |
| <span data-ttu-id="6de29-146">Windows Storage Server 2012 和最新的 SP</span><span class="sxs-lookup"><span data-stu-id="6de29-146">Windows Storage Server 2012 and latest SPs</span></span> |<span data-ttu-id="6de29-147">64 位元</span><span class="sxs-lookup"><span data-stu-id="6de29-147">64 bit</span></span> |<span data-ttu-id="6de29-148">Standard、Workgroup</span><span class="sxs-lookup"><span data-stu-id="6de29-148">Standard, Workgroup</span></span> |

<span data-ttu-id="6de29-149">您可以使用 Windows Server Deduplication 為 DPM 儲存體刪除重複資料。</span><span class="sxs-lookup"><span data-stu-id="6de29-149">You can deduplicate the DPM storage using Windows Server Deduplication.</span></span> <span data-ttu-id="6de29-150">深入了解在 Hyper-V VM 中部署時， [DPM 和重複資料刪除](https://technet.microsoft.com/library/dn891438.aspx) 如何搭配運作。</span><span class="sxs-lookup"><span data-stu-id="6de29-150">Learn more about how [DPM and deduplication](https://technet.microsoft.com/library/dn891438.aspx) work together when deployed in Hyper-V VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="6de29-151">Azure 備份伺服器的設計目的是在專用、單一用途的伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="6de29-151">Azure Backup Server is designed to run on a dedicated, single-purpose server.</span></span> <span data-ttu-id="6de29-152">您無法在下列位置安裝 Azure 備份伺服器︰</span><span class="sxs-lookup"><span data-stu-id="6de29-152">You cannot install Azure Backup Server on:</span></span>
> - <span data-ttu-id="6de29-153">執行為網域控制站的電腦</span><span class="sxs-lookup"><span data-stu-id="6de29-153">A computer running as a domain controller</span></span>
> - <span data-ttu-id="6de29-154">安裝應用程式伺服器角色所在的電腦</span><span class="sxs-lookup"><span data-stu-id="6de29-154">A computer on which the Application Server role is installed</span></span>
> - <span data-ttu-id="6de29-155">本身是 System Center Operations Manager 管理群組的電腦</span><span class="sxs-lookup"><span data-stu-id="6de29-155">A computer that is a System Center Operations Manager management server</span></span>
> - <span data-ttu-id="6de29-156">Exchange Server 執行所在的電腦</span><span class="sxs-lookup"><span data-stu-id="6de29-156">A computer on which Exchange Server is running</span></span>
> - <span data-ttu-id="6de29-157">本身是叢集節點的電腦</span><span class="sxs-lookup"><span data-stu-id="6de29-157">A computer that is a node of a cluster</span></span>

<span data-ttu-id="6de29-158">Azure 備份伺服器一律加入網域。</span><span class="sxs-lookup"><span data-stu-id="6de29-158">Always join Azure Backup Server to a domain.</span></span> <span data-ttu-id="6de29-159">如果您打算將伺服器移到不同的網域，建議您先將伺服器加入新網域，再安裝 Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="6de29-159">If you plan to move the server to a different domain, it is recommended that you join the server to the new domain before installing Azure Backup Server.</span></span> <span data-ttu-id="6de29-160">若在部署後將現有的 Azure 備份伺服器機器移至新網域，該動作將「不受支援」 。</span><span class="sxs-lookup"><span data-stu-id="6de29-160">Moving an existing Azure Backup Server machine to a new domain after deployment is *not supported*.</span></span>

## <a name="2-recovery-services-vault"></a><span data-ttu-id="6de29-161">2.復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="6de29-161">2. Recovery Services vault</span></span>
<span data-ttu-id="6de29-162">無論您要將備份資料傳送至 Azure，還是將其保存在本機上，軟體都必須連接到 Azure。</span><span class="sxs-lookup"><span data-stu-id="6de29-162">Whether you send backup data to Azure or keep it locally, the software needs to be connected to Azure.</span></span> <span data-ttu-id="6de29-163">明確而言，Azure 備份伺服器機器必須向復原服務保存庫註冊。</span><span class="sxs-lookup"><span data-stu-id="6de29-163">To be more specific, the Azure Backup Server machine needs to be registered with a recovery services vault.</span></span>

<span data-ttu-id="6de29-164">若要建立復原服務保存庫：</span><span class="sxs-lookup"><span data-stu-id="6de29-164">To create a recovery services vault:</span></span>

1. <span data-ttu-id="6de29-165">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6de29-165">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6de29-166">在 [中樞] 功能表上按一下 [瀏覽]，然後在資源清單中輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="6de29-166">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="6de29-167">當您開始輸入時，清單會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="6de29-167">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="6de29-168">按一下 [復原服務保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-168">Click **Recovery Services vault**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    <span data-ttu-id="6de29-170">隨即會顯示 [復原服務保存庫] 清單。</span><span class="sxs-lookup"><span data-stu-id="6de29-170">The list of Recovery Services vaults is displayed.</span></span>
3. <span data-ttu-id="6de29-171">在 [復原服務保存庫] 功能表上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6de29-171">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![建立復原服務保存庫的步驟 2](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    <span data-ttu-id="6de29-173">[復原服務保存庫] 刀鋒視窗隨即開啟，並提示您提供 [名稱]、[訂用帳戶]、[資源群組] 和 [位置]。</span><span class="sxs-lookup"><span data-stu-id="6de29-173">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![建立復原服務保存庫的步驟 5](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. <span data-ttu-id="6de29-175">在 [名稱] 中，輸入易記名稱來識別保存庫。</span><span class="sxs-lookup"><span data-stu-id="6de29-175">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="6de29-176">必須是 Azure 訂用帳戶中唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="6de29-176">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="6de29-177">輸入包含 2 到 50 個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="6de29-177">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="6de29-178">該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="6de29-178">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>
5. <span data-ttu-id="6de29-179">按一下 [訂用帳戶]  以查看可用的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="6de29-179">Click **Subscription** to see the available list of subscriptions.</span></span> <span data-ttu-id="6de29-180">如果您不確定要使用哪個訂用帳戶，請使用預設 (或建議) 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6de29-180">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="6de29-181">只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。</span><span class="sxs-lookup"><span data-stu-id="6de29-181">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>
6. <span data-ttu-id="6de29-182">按一下 [資源群組] 以查看可用的資源群組清單，或按一下 [新增] 以建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6de29-182">Click **Resource group** to see the available list of Resource groups, or click **New** to create a new Resource group.</span></span> <span data-ttu-id="6de29-183">如需資源群組的完整資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6de29-183">For complete information on Resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
7. <span data-ttu-id="6de29-184">按一下 [位置]  以選取保存庫的地理區域。</span><span class="sxs-lookup"><span data-stu-id="6de29-184">Click **Location** to select the geographic region for the vault.</span></span>
8. <span data-ttu-id="6de29-185">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-185">Click **Create**.</span></span> <span data-ttu-id="6de29-186">要等復原服務保存庫建立好，可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="6de29-186">It can take a while for the Recovery Services vault to be created.</span></span> <span data-ttu-id="6de29-187">請監視入口網站右上方區域中的狀態通知。</span><span class="sxs-lookup"><span data-stu-id="6de29-187">Monitor the status notifications in the upper right-hand area in the portal.</span></span>
   <span data-ttu-id="6de29-188">保存庫一旦建立好，就會在入口網站中開啟。</span><span class="sxs-lookup"><span data-stu-id="6de29-188">Once your vault is created, it opens in the portal.</span></span>

### <a name="set-storage-replication"></a><span data-ttu-id="6de29-189">設定儲存體複寫</span><span class="sxs-lookup"><span data-stu-id="6de29-189">Set Storage Replication</span></span>
<span data-ttu-id="6de29-190">儲存體複寫選項有異地備援儲存體和本地備援儲存體可供您選擇。</span><span class="sxs-lookup"><span data-stu-id="6de29-190">The storage replication option allows you to choose between geo-redundant storage and locally redundant storage.</span></span> <span data-ttu-id="6de29-191">根據預設，保存庫具有異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="6de29-191">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="6de29-192">如果這個保存庫是您的主要保存庫，儲存體選項請保持設定為異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="6de29-192">If this vault is your primary vault, leave the storage option set to geo-redundant storage.</span></span> <span data-ttu-id="6de29-193">如果您想要更便宜但不持久的選項，請選擇本地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="6de29-193">Choose locally redundant storage if you want a cheaper option that isn't quite as durable.</span></span> <span data-ttu-id="6de29-194">在 [Azure 儲存體複寫概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="6de29-194">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in the [Azure Storage replication overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="6de29-195">若要編輯儲存體複寫設定︰</span><span class="sxs-lookup"><span data-stu-id="6de29-195">To edit the storage replication setting:</span></span>

1. <span data-ttu-id="6de29-196">選取保存庫以開啟保存庫儀表板和 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6de29-196">Select your vault to open the vault dashboard and the Settings blade.</span></span> <span data-ttu-id="6de29-197">如果 [設定] 刀鋒視窗未開啟，請按一下保存庫儀表板中的 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="6de29-197">If the **Settings** blade doesn't open, click **All settings** in the vault dashboard.</span></span>
2. <span data-ttu-id="6de29-198">在 [設定] 刀鋒視窗上按一下 [備份基礎結構]  >  [備份設定]，開啟 [備份設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6de29-198">On the **Settings** blade, click **Backup Infrastructure** > **Backup Configuration** to open the **Backup Configuration** blade.</span></span> <span data-ttu-id="6de29-199">在 [備份設定]  刀鋒視窗上，選擇保存庫的儲存體複寫選項。</span><span class="sxs-lookup"><span data-stu-id="6de29-199">On the **Backup Configuration** blade, choose the storage replication option for your vault.</span></span>

    ![備份保存庫的清單](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    <span data-ttu-id="6de29-201">選擇好保存庫的儲存體選項後，就可以開始建立 VM 與保存庫的關聯。</span><span class="sxs-lookup"><span data-stu-id="6de29-201">After choosing the storage option for your vault, you are ready to associate the VM with the vault.</span></span> <span data-ttu-id="6de29-202">若要開始關聯，請探索及註冊 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6de29-202">To begin the association, you should discover and register the Azure virtual machines.</span></span>

## <a name="3-software-package"></a><span data-ttu-id="6de29-203">3.軟體封裝</span><span class="sxs-lookup"><span data-stu-id="6de29-203">3. Software package</span></span>
### <a name="downloading-the-software-package"></a><span data-ttu-id="6de29-204">下載軟體封裝</span><span class="sxs-lookup"><span data-stu-id="6de29-204">Downloading the software package</span></span>
1. <span data-ttu-id="6de29-205">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6de29-205">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6de29-206">如果您已開啟復原服務保存庫，請繼續步驟 3。</span><span class="sxs-lookup"><span data-stu-id="6de29-206">If you already have a Recovery Services vault open, proceed to step 3.</span></span> <span data-ttu-id="6de29-207">如果您並未開啟復原服務保存庫，但位於 Azure 入口網站中，請在 [中樞] 功能表上按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-207">If you do not have a Recovery Services vault open, but are in the Azure portal, on the Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="6de29-208">在資源清單中輸入 **復原服務**。</span><span class="sxs-lookup"><span data-stu-id="6de29-208">In the list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="6de29-209">當您開始輸入時，清單將會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="6de29-209">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="6de29-210">當您看到 [復原服務保存庫] 時，請按一下它。</span><span class="sxs-lookup"><span data-stu-id="6de29-210">When you see **Recovery Services vaults**, click it.</span></span>

     ![建立復原服務保存庫的步驟 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     <span data-ttu-id="6de29-212">隨即會出現 [復原服務保存庫] 清單。</span><span class="sxs-lookup"><span data-stu-id="6de29-212">The list of Recovery Services vaults appears.</span></span>
   * <span data-ttu-id="6de29-213">在 [復原服務保存庫] 清單中選取保存庫。</span><span class="sxs-lookup"><span data-stu-id="6de29-213">From the list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="6de29-214">選取的保存庫儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6de29-214">The selected vault dashboard opens.</span></span>

     ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. <span data-ttu-id="6de29-216">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="6de29-216">The **Settings** blade opens up by default.</span></span> <span data-ttu-id="6de29-217">如果該刀鋒視窗未開啟，請按一下 [設定]  以開啟 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6de29-217">If it is closed, click on **Settings** to open the settings blade.</span></span>

    ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. <span data-ttu-id="6de29-219">按一下 [備份] 以開啟 [開始使用] 精靈。</span><span class="sxs-lookup"><span data-stu-id="6de29-219">Click **Backup** to open the Getting Started wizard.</span></span>

    ![備份開始使用](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    <span data-ttu-id="6de29-221">在開啟的 [開始使用備份] 刀鋒視窗中，系統會自動選取 [備份目標]。</span><span class="sxs-lookup"><span data-stu-id="6de29-221">In the **Getting Started with backup** blade that opens, **Backup Goals** will be auto-selected.</span></span>

    ![Backup-goals-default-opened](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. <span data-ttu-id="6de29-223">在 [備份目標] 刀鋒視窗中，從 [您的工作負載在何處執行] 功能表中，選取 [內部部署]。</span><span class="sxs-lookup"><span data-stu-id="6de29-223">In the **Backup Goal** blade, from the **Where is your workload running** menu, select **On-premises**.</span></span>

    ![內部部署和做為目標的工作負載](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    <span data-ttu-id="6de29-225">從 [你想要備份哪些項目？] 下拉式功能表中，選取您要使用 Azure 備份伺服器保護的工作負載，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6de29-225">From the **What do you want to backup?** drop-down menu, select the workloads you want to protect using Azure Backup Server, and then click **OK**.</span></span>

    <span data-ttu-id="6de29-226">[開始使用備份功能] 精靈會切換 [準備基礎結構] 選項以將工作負載備份至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6de29-226">The **Getting Started with backup** wizard switches the **Prepare infrastructure** option to back up workloads to Azure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6de29-227">如果您只想要備份檔案和資料夾，我們建議使用 Azure 備份代理程式並遵循[初步了解：備份檔案和資料夾](backup-try-azure-backup-in-10-mins.md)一文中的指引。</span><span class="sxs-lookup"><span data-stu-id="6de29-227">If you only want to back up files and folders, we recommend using the Azure Backup agent and following the guidance in the article, [First look: back up files and folders](backup-try-azure-backup-in-10-mins.md).</span></span> <span data-ttu-id="6de29-228">如果您想要保護比檔案和資料夾更多的工作負載，或未來有擴充保護需求的規劃，請選取那些工作負載。</span><span class="sxs-lookup"><span data-stu-id="6de29-228">If you are going to protect more than files and folders, or you are planning to expand the protection needs in the future, select those workloads.</span></span>
   >
   >

    ![開始使用精靈變更](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. <span data-ttu-id="6de29-230">在開啟的 [準備基礎結構] 刀鋒視窗中，按一下可供安裝 Azure 備份伺服器和下載保存庫認證的 [下載] 連結。</span><span class="sxs-lookup"><span data-stu-id="6de29-230">In the **Prepare infrastructure** blade that opens, click the **Download** links for Install Azure Backup Server and Download vault credentials.</span></span> <span data-ttu-id="6de29-231">在將 Azure 備份伺服器註冊到復原服務保存庫期間，您必須使用保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="6de29-231">You use the vault credentials during registration of Azure Backup Server to the recovery services vault.</span></span> <span data-ttu-id="6de29-232">連結會使您進入可下載軟體套件的 [下載中心]。</span><span class="sxs-lookup"><span data-stu-id="6de29-232">The links take you to the Download Center where the software package can be downloaded.</span></span>

    ![準備用於 Azure 備份伺服器的基礎結構](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. <span data-ttu-id="6de29-234">選取所有檔案，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-234">Select all the files and click **Next**.</span></span> <span data-ttu-id="6de29-235">下載 [Microsoft Azure 備份] 下載頁面中的所有檔案，並將所有檔案放在相同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6de29-235">Download all the files coming in from the Microsoft Azure Backup download page, and place all the files in the same folder.</span></span>

    ![下載中心 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    <span data-ttu-id="6de29-237">因為所有檔案的下載大小合計 > 3G，在 10Mbps 下載連結上可能需要 60 分鐘才能完成下載。</span><span class="sxs-lookup"><span data-stu-id="6de29-237">Since the download size of all the files together is > 3G, on a 10Mbps download link it may take up to 60 minutes for the download to complete.</span></span>

### <a name="extracting-the-software-package"></a><span data-ttu-id="6de29-238">將軟體封裝解壓縮</span><span class="sxs-lookup"><span data-stu-id="6de29-238">Extracting the software package</span></span>
<span data-ttu-id="6de29-239">下載所有檔案之後，按一下 [MicrosoftAzureBackupInstaller.exe] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-239">After you've downloaded all the files, click **MicrosoftAzureBackupInstaller.exe**.</span></span> <span data-ttu-id="6de29-240">這會啟動 [Microsoft Azure 備份安裝精靈]  ，並將安裝程式檔案解壓縮至您所指定的位置。</span><span class="sxs-lookup"><span data-stu-id="6de29-240">This will start the **Microsoft Azure Backup Setup Wizard** to extract the setup files to a location specified by you.</span></span> <span data-ttu-id="6de29-241">繼續執行精靈，然後按一下 [解壓縮]  按鈕，以開始解壓縮程序。</span><span class="sxs-lookup"><span data-stu-id="6de29-241">Continue through the wizard and click on the **Extract** button to begin the extraction process.</span></span>

> [!WARNING]
> <span data-ttu-id="6de29-242">至少 4 GB 的可用空間，才能將安裝程式檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="6de29-242">At least 4GB of free space is required to extract the setup files.</span></span>
>
>

![Microsoft Azure 備份安裝精靈](./media/backup-azure-microsoft-azure-backup/extract/03.png)

<span data-ttu-id="6de29-244">解壓縮程序完成之後，請選取可啟動剛解壓縮 setup.exe 的方塊，以開始安裝 Microsoft Azure 備份伺服器，然後按一下 [完成] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6de29-244">Once the extraction process complete, check the box to launch the freshly extracted *setup.exe* to begin installing Microsoft Azure Backup Server and click on the **Finish** button.</span></span>

### <a name="installing-the-software-package"></a><span data-ttu-id="6de29-245">安裝軟體封裝</span><span class="sxs-lookup"><span data-stu-id="6de29-245">Installing the software package</span></span>
1. <span data-ttu-id="6de29-246">按一下 [Microsoft Azure 備份]  啟動安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="6de29-246">Click **Microsoft Azure Backup** to launch the setup wizard.</span></span>

    ![Microsoft Azure 備份安裝精靈](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. <span data-ttu-id="6de29-248">在 [歡迎使用] 畫面上按 [下一步]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6de29-248">On the Welcome screen click the **Next** button.</span></span> <span data-ttu-id="6de29-249">這會讓您進入 [必要條件檢查]  區段。</span><span class="sxs-lookup"><span data-stu-id="6de29-249">This takes you to the *Prerequisite Checks* section.</span></span> <span data-ttu-id="6de29-250">在此畫面上按一下 [檢查]，以判斷是否符合 Azure 備份伺服器的硬體和軟體必要條件。</span><span class="sxs-lookup"><span data-stu-id="6de29-250">On this screen, click **Check** to determine if the hardware and software prerequisites for Azure Backup Server have been met.</span></span> <span data-ttu-id="6de29-251">如果完全符合所有必要條件，您會看到訊息指出機器符合需求。</span><span class="sxs-lookup"><span data-stu-id="6de29-251">If all prerequisites are met successfully, you will see a message indicating that the machine meets the requirements.</span></span> <span data-ttu-id="6de29-252">按 [下一步]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6de29-252">Click on the **Next** button.</span></span>

    ![Azure 備份伺服器 - 歡迎使用和必要條件檢查](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. <span data-ttu-id="6de29-254">Microsoft Azure 備份伺服器需要 SQL Server 標準，而 Azure 備份伺服器安裝封裝在必要時會隨附適當的 SQL Server 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="6de29-254">Microsoft Azure Backup Server requires SQL Server Standard, and the Azure Backup Server installation package comes bundled with the appropriate SQL Server binaries needed.</span></span> <span data-ttu-id="6de29-255">在進行新的 Azure 備份伺服器安裝時，您應該選擇 [在此安裝中安裝新的 SQL Server 執行個體]，然後按一下 [檢查並安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6de29-255">When starting with a new Azure Backup Server installation, you should pick the option **Install new Instance of SQL Server with this Setup** and click the **Check and Install** button.</span></span> <span data-ttu-id="6de29-256">成功安裝必要條件後，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-256">Once the prerequisites are successfully installed, click **Next**.</span></span>

    ![Azure 備份伺服器 - SQL 檢查](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    <span data-ttu-id="6de29-258">如果發生失敗且建議您重新啟動電腦，請依指示進行，然後按一下 [再檢查一次] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-258">If a failure occurs with a recommendation to restart the machine, do so and click **Check Again**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6de29-259">Azure 備份伺服器不會使用遠端 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="6de29-259">Azure Backup Server will not work with a remote SQL Server instance.</span></span> <span data-ttu-id="6de29-260">Azure 備份伺服器所使用的執行個體必須是本機的。</span><span class="sxs-lookup"><span data-stu-id="6de29-260">The instance being used by Azure Backup Server needs to be local.</span></span>
   >
   >
4. <span data-ttu-id="6de29-261">提供 Microsoft Azure 備份伺服器檔案的安裝位置，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-261">Provide a location for the installation of Microsoft Azure Backup server files and click **Next**.</span></span>

    ![Microsoft Azure 備份必要條件 2](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    <span data-ttu-id="6de29-263">備份至 Azure 需要暫存位置。</span><span class="sxs-lookup"><span data-stu-id="6de29-263">The scratch location is a requirement for back up to Azure.</span></span> <span data-ttu-id="6de29-264">請確保暫存位置至少為打算備份至雲端的資料的 5%。</span><span class="sxs-lookup"><span data-stu-id="6de29-264">Ensure the scratch location is at least 5% of the data planned to be backed up to the cloud.</span></span> <span data-ttu-id="6de29-265">在磁碟保護方面，安裝完成之後必須設定獨立的磁碟。</span><span class="sxs-lookup"><span data-stu-id="6de29-265">For disk protection, separate disks need to be configured once the installation completes.</span></span> <span data-ttu-id="6de29-266">如需有關存放集區的詳細資訊，請參閱 [設定存放集區和磁碟儲存體](https://technet.microsoft.com/library/hh758075.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6de29-266">For more information regarding storage pools, see [Configure storage pools and disk storage](https://technet.microsoft.com/library/hh758075.aspx).</span></span>
5. <span data-ttu-id="6de29-267">為受限的本機使用者帳戶提供強式密碼，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6de29-267">Provide a strong password for restricted local user accounts and click **Next**.</span></span>

    ![Microsoft Azure 備份必要條件 2](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. <span data-ttu-id="6de29-269">選取是否要使用 *Microsoft Update* 檢查更新，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6de29-269">Select whether you want to use *Microsoft Update* to check for updates and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6de29-270">建議讓 Windows Update 重新導向至 Microsoft Update，此網站為 Windows 和 Microsoft Azure 備份伺服器等其他產品提供安全性和重要更新。</span><span class="sxs-lookup"><span data-stu-id="6de29-270">We recommend having Windows Update redirect to Microsoft Update, which offers security and important updates for Windows and other products like Microsoft Azure Backup Server.</span></span>
   >
   >

    ![Microsoft Azure 備份必要條件 2](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. <span data-ttu-id="6de29-272">檢閱「設定值摘要」，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="6de29-272">Review the *Summary of Settings* and click **Install**.</span></span>

    ![Microsoft Azure 備份必要條件 2](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. <span data-ttu-id="6de29-274">安裝分階段執行。</span><span class="sxs-lookup"><span data-stu-id="6de29-274">The installation happens in phases.</span></span> <span data-ttu-id="6de29-275">在第一個階段中，會將 Microsoft Azure 復原服務代理程式安裝在伺服器上。</span><span class="sxs-lookup"><span data-stu-id="6de29-275">In the first phase the Microsoft Azure Recovery Services Agent is installed on the server.</span></span> <span data-ttu-id="6de29-276">精靈也會檢查網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="6de29-276">The wizard also checks for Internet connectivity.</span></span> <span data-ttu-id="6de29-277">如果可連線至網際網路，您可以繼續安裝，否則必須提供 Proxy 詳細資料來連線到網際網路。</span><span class="sxs-lookup"><span data-stu-id="6de29-277">If Internet connectivity is available you can proceed with installation, if not, you need to provide proxy details to connect to the Internet.</span></span>

    <span data-ttu-id="6de29-278">下一個步驟是設定 Microsoft Azure 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="6de29-278">The next step is to configure the Microsoft Azure Recovery Services Agent.</span></span> <span data-ttu-id="6de29-279">在設定的過程中，您將必須提供保存庫認證，以向復原服務保存庫註冊機器。</span><span class="sxs-lookup"><span data-stu-id="6de29-279">As a part of the configuration, you will have to provide your vault credentials to register the machine to the recovery services vault.</span></span> <span data-ttu-id="6de29-280">您也須提供複雜密碼來加密/解密 Azure 與您的內部部署之間所傳送的資料。</span><span class="sxs-lookup"><span data-stu-id="6de29-280">You will also provide a passphrase to encrypt/decrypt the data sent between Azure and your premises.</span></span> <span data-ttu-id="6de29-281">您可以自動產生複雜密碼，或提供您自己的複雜密碼，最少 16 個字元。</span><span class="sxs-lookup"><span data-stu-id="6de29-281">You can automatically generate a passphrase or provide your own minimum 16-character passphrase.</span></span> <span data-ttu-id="6de29-282">繼續執行精靈，直到代理程式完成設定。</span><span class="sxs-lookup"><span data-stu-id="6de29-282">Continue with the wizard until the agent has been configured.</span></span>

    ![Azure 備份伺服器必要條件 2](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. <span data-ttu-id="6de29-284">Microsoft Azure 備份伺服器順利完成註冊後，整體安裝精靈會繼續安裝及設定 SQL Server 和 Azure 備份伺服器的元件。</span><span class="sxs-lookup"><span data-stu-id="6de29-284">Once registration of the Microsoft Azure Backup server successfully completes, the overall setup wizard proceeds to the installation and configuration of SQL Server and the Azure Backup Server components.</span></span> <span data-ttu-id="6de29-285">SQL Server 元件安裝完成後，會安裝 Azure 備份伺服器元件。</span><span class="sxs-lookup"><span data-stu-id="6de29-285">Once the SQL Server component installation completes, the Azure Backup Server components are installed.</span></span>

    ![Azure 備份伺服器](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

<span data-ttu-id="6de29-287">當安裝步驟完成時，產品的桌面圖示也將一併建立完成。</span><span class="sxs-lookup"><span data-stu-id="6de29-287">When the installation step has completed, the product's desktop icons will have been created as well.</span></span> <span data-ttu-id="6de29-288">只要按兩下該圖示，即可啟動產品。</span><span class="sxs-lookup"><span data-stu-id="6de29-288">Just double-click the icon to launch the product.</span></span>

### <a name="add-backup-storage"></a><span data-ttu-id="6de29-289">新增備份儲存體</span><span class="sxs-lookup"><span data-stu-id="6de29-289">Add backup storage</span></span>
<span data-ttu-id="6de29-290">第一個備份複本會保存在連接至 Azure 備份伺服器機器的儲存體上。</span><span class="sxs-lookup"><span data-stu-id="6de29-290">The first backup copy is kept on storage attached to the Azure Backup Server machine.</span></span> <span data-ttu-id="6de29-291">如需有關新增磁碟的詳細資訊，請參閱 [設定存放集區和磁碟儲存體](https://technet.microsoft.com/library/hh758075.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6de29-291">For more information about adding disks, see [Configure storage pools and disk storage](https://technet.microsoft.com/library/hh758075.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6de29-292">即使您打算將資料傳送至 Azure，也必須新增備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="6de29-292">You need to add backup storage even if you plan to send data to Azure.</span></span> <span data-ttu-id="6de29-293">在目前的「Azure 備份伺服器」架構中，「Azure 備份」保存庫會保存資料的「第二個」  複本，而本機儲存體則是保存第一個 (必要的) 備份複本。</span><span class="sxs-lookup"><span data-stu-id="6de29-293">In the current architecture of Azure Backup Server, the Azure Backup vault holds the *second* copy of the data while the local storage holds the first (and mandatory) backup copy.</span></span>
>
>

## <a name="4-network-connectivity"></a><span data-ttu-id="6de29-294">4.網路連線</span><span class="sxs-lookup"><span data-stu-id="6de29-294">4. Network connectivity</span></span>
<span data-ttu-id="6de29-295">Azure 備份伺服器需要連線至 Azure 備份服務，產品才能順利運作。</span><span class="sxs-lookup"><span data-stu-id="6de29-295">Azure Backup Server requires connectivity to the Azure Backup service for the product to work successfully.</span></span> <span data-ttu-id="6de29-296">若要驗證機器是否連接至 Azure，請在Azure 備份伺服器 PowerShell 主控台中使用 ```Get-DPMCloudConnection``` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6de29-296">To validate whether the machine has the connectivity to Azure, use the ```Get-DPMCloudConnection``` cmdlet in the Azure Backup Server PowerShell console.</span></span> <span data-ttu-id="6de29-297">如果 Cmdlet 的輸出為 TRUE，表示連線存在，否則沒有連線。</span><span class="sxs-lookup"><span data-stu-id="6de29-297">If the output of the cmdlet is TRUE then connectivity exists, else there is no connectivity.</span></span>

<span data-ttu-id="6de29-298">同時，Azure 訂用帳戶也必須處於狀況良好狀態。</span><span class="sxs-lookup"><span data-stu-id="6de29-298">At the same time, the Azure subscription needs to be in a healthy state.</span></span> <span data-ttu-id="6de29-299">若您想了解訂用帳戶狀態並加以管理，請登入 [訂用帳戶入口網站](https://account.windowsazure.com/Subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="6de29-299">To find out the state of your subscription and to manage it, log in to the [subscription portal](https://account.windowsazure.com/Subscriptions).</span></span>

<span data-ttu-id="6de29-300">在您了解 Azure 連線和 Azure 訂用帳戶的狀態後，您可以使用下表來確認提供的備份/還原功能會受到哪些影響。</span><span class="sxs-lookup"><span data-stu-id="6de29-300">Once you know the state of the Azure connectivity and of the Azure subscription, you can use the table below to find out the impact on the backup/restore functionality offered.</span></span>

| <span data-ttu-id="6de29-301">連線狀態</span><span class="sxs-lookup"><span data-stu-id="6de29-301">Connectivity State</span></span> | <span data-ttu-id="6de29-302">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="6de29-302">Azure Subscription</span></span> | <span data-ttu-id="6de29-303">備份至 Azure</span><span class="sxs-lookup"><span data-stu-id="6de29-303">Back up to Azure</span></span> | <span data-ttu-id="6de29-304">備份到磁碟</span><span class="sxs-lookup"><span data-stu-id="6de29-304">Back up to disk</span></span> | <span data-ttu-id="6de29-305">從 Azure 還原</span><span class="sxs-lookup"><span data-stu-id="6de29-305">Restore from Azure</span></span> | <span data-ttu-id="6de29-306">從磁碟還原</span><span class="sxs-lookup"><span data-stu-id="6de29-306">Restore from disk</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6de29-307">連線</span><span class="sxs-lookup"><span data-stu-id="6de29-307">Connected</span></span> |<span data-ttu-id="6de29-308">Active</span><span class="sxs-lookup"><span data-stu-id="6de29-308">Active</span></span> |<span data-ttu-id="6de29-309">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-309">Allowed</span></span> |<span data-ttu-id="6de29-310">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-310">Allowed</span></span> |<span data-ttu-id="6de29-311">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-311">Allowed</span></span> |<span data-ttu-id="6de29-312">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-312">Allowed</span></span> |
| <span data-ttu-id="6de29-313">連線</span><span class="sxs-lookup"><span data-stu-id="6de29-313">Connected</span></span> |<span data-ttu-id="6de29-314">已過期</span><span class="sxs-lookup"><span data-stu-id="6de29-314">Expired</span></span> |<span data-ttu-id="6de29-315">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-315">Stopped</span></span> |<span data-ttu-id="6de29-316">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-316">Stopped</span></span> |<span data-ttu-id="6de29-317">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-317">Allowed</span></span> |<span data-ttu-id="6de29-318">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-318">Allowed</span></span> |
| <span data-ttu-id="6de29-319">連線</span><span class="sxs-lookup"><span data-stu-id="6de29-319">Connected</span></span> |<span data-ttu-id="6de29-320">已取消佈建</span><span class="sxs-lookup"><span data-stu-id="6de29-320">Deprovisioned</span></span> |<span data-ttu-id="6de29-321">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-321">Stopped</span></span> |<span data-ttu-id="6de29-322">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-322">Stopped</span></span> |<span data-ttu-id="6de29-323">已停止且已刪除 Azure 復原點</span><span class="sxs-lookup"><span data-stu-id="6de29-323">Stopped and Azure recovery points deleted</span></span> |<span data-ttu-id="6de29-324">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-324">Stopped</span></span> |
| <span data-ttu-id="6de29-325">連線中斷 > 15 天</span><span class="sxs-lookup"><span data-stu-id="6de29-325">Lost connectivity > 15 days</span></span> |<span data-ttu-id="6de29-326">Active</span><span class="sxs-lookup"><span data-stu-id="6de29-326">Active</span></span> |<span data-ttu-id="6de29-327">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-327">Stopped</span></span> |<span data-ttu-id="6de29-328">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-328">Stopped</span></span> |<span data-ttu-id="6de29-329">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-329">Allowed</span></span> |<span data-ttu-id="6de29-330">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-330">Allowed</span></span> |
| <span data-ttu-id="6de29-331">連線中斷 > 15 天</span><span class="sxs-lookup"><span data-stu-id="6de29-331">Lost connectivity > 15 days</span></span> |<span data-ttu-id="6de29-332">已過期</span><span class="sxs-lookup"><span data-stu-id="6de29-332">Expired</span></span> |<span data-ttu-id="6de29-333">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-333">Stopped</span></span> |<span data-ttu-id="6de29-334">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-334">Stopped</span></span> |<span data-ttu-id="6de29-335">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-335">Allowed</span></span> |<span data-ttu-id="6de29-336">允許</span><span class="sxs-lookup"><span data-stu-id="6de29-336">Allowed</span></span> |
| <span data-ttu-id="6de29-337">連線中斷 > 15 天</span><span class="sxs-lookup"><span data-stu-id="6de29-337">Lost connectivity > 15 days</span></span> |<span data-ttu-id="6de29-338">已取消佈建</span><span class="sxs-lookup"><span data-stu-id="6de29-338">Deprovisioned</span></span> |<span data-ttu-id="6de29-339">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-339">Stopped</span></span> |<span data-ttu-id="6de29-340">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-340">Stopped</span></span> |<span data-ttu-id="6de29-341">已停止且已刪除 Azure 復原點</span><span class="sxs-lookup"><span data-stu-id="6de29-341">Stopped and Azure recovery points deleted</span></span> |<span data-ttu-id="6de29-342">已停止</span><span class="sxs-lookup"><span data-stu-id="6de29-342">Stopped</span></span> |

### <a name="recovering-from-loss-of-connectivity"></a><span data-ttu-id="6de29-343">從連線中斷的情況復原</span><span class="sxs-lookup"><span data-stu-id="6de29-343">Recovering from loss of connectivity</span></span>
<span data-ttu-id="6de29-344">如果您有防火牆或 Proxy 以致無法存取 Azure，您必須將防火牆/Proxy 設定檔中的下列網域位址列入允許清單中：</span><span class="sxs-lookup"><span data-stu-id="6de29-344">If you have a firewall or a proxy that is preventing access to Azure, you need to whitelist the following domain addresses in the firewall/proxy profile:</span></span>

* <span data-ttu-id="6de29-345">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="6de29-345">www.msftncsi.com</span></span>
* <span data-ttu-id="6de29-346">\*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6de29-346">\*.Microsoft.com</span></span>
* <span data-ttu-id="6de29-347">\*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="6de29-347">\*.WindowsAzure.com</span></span>
* <span data-ttu-id="6de29-348">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6de29-348">\*.microsoftonline.com</span></span>
* <span data-ttu-id="6de29-349">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="6de29-349">\*.windows.net</span></span>

<span data-ttu-id="6de29-350">在 Azure 的連線已還原至 Azure 備份伺服器機器之後，可執行的作業將取決於 Azure 訂用帳戶狀態。</span><span class="sxs-lookup"><span data-stu-id="6de29-350">Once connectivity to Azure has been restored to the Azure Backup Server machine, the operations that can be performed are determined by the Azure subscription state.</span></span> <span data-ttu-id="6de29-351">上表詳細列出機器「已連接」之後所允許之作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6de29-351">The table above has details about the operations allowed once the machine is "Connected".</span></span>

### <a name="handling-subscription-states"></a><span data-ttu-id="6de29-352">處理訂用帳戶狀態</span><span class="sxs-lookup"><span data-stu-id="6de29-352">Handling subscription states</span></span>
<span data-ttu-id="6de29-353">您可以將 Azure 訂用帳戶從「已過期」或「已取消佈建」狀態變更為「作用中」狀態。</span><span class="sxs-lookup"><span data-stu-id="6de29-353">It is possible to take an Azure subscription from an *Expired* or *Deprovisioned* state to the *Active* state.</span></span> <span data-ttu-id="6de29-354">不過，當狀態不是「作用中」 時，此動作會對產品的行為造成某些影響：</span><span class="sxs-lookup"><span data-stu-id="6de29-354">However this has some implications on the product behavior while the state is not *Active*:</span></span>

* <span data-ttu-id="6de29-355">「已取消佈建」  的訂用帳戶在取消佈建的這段期間會失去功能。</span><span class="sxs-lookup"><span data-stu-id="6de29-355">A *Deprovisioned* subscription loses functionality for the period that it is deprovisioned.</span></span> <span data-ttu-id="6de29-356">切換為「作用中」 時，就會恢復產品的備份/還原功能。</span><span class="sxs-lookup"><span data-stu-id="6de29-356">On turning *Active*, the product functionality of backup/restore is revived.</span></span> <span data-ttu-id="6de29-357">此外，只要以夠大的保留期間來保存，也可以擷取本機磁碟上的備份資料。</span><span class="sxs-lookup"><span data-stu-id="6de29-357">The backup data on the local disk also can be retrieved if it was kept with a sufficiently large retention period.</span></span> <span data-ttu-id="6de29-358">不過，一旦訂用帳戶進入「已取消佈建」  狀態，Azure 中的備份資料便會遺失而無法復原。</span><span class="sxs-lookup"><span data-stu-id="6de29-358">However, the backup data in Azure is irretrievably lost once the subscription enters the *Deprovisioned* state.</span></span>
* <span data-ttu-id="6de29-359">「已過期」的訂用帳戶只有在恢復「作用中」狀態之前會失去功能。</span><span class="sxs-lookup"><span data-stu-id="6de29-359">An *Expired* subscription only loses functionality for until it has been made *Active* again.</span></span> <span data-ttu-id="6de29-360">任何針對訂用帳戶處於「已過期」  期間所排定的備份，都不會執行。</span><span class="sxs-lookup"><span data-stu-id="6de29-360">Any backups scheduled for the period that the subscription was *Expired* will not run.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6de29-361">疑難排解</span><span class="sxs-lookup"><span data-stu-id="6de29-361">Troubleshooting</span></span>
<span data-ttu-id="6de29-362">如果 Microsoft Azure 備份伺服器在安裝階段 (或是備份或還原) 失敗且出現錯誤，請參閱這份[錯誤碼文件](https://support.microsoft.com/kb/3041338)，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6de29-362">If Microsoft Azure Backup server fails with errors during the setup phase (or backup or restore), refer to this [error codes document](https://support.microsoft.com/kb/3041338)  for more information.</span></span>
<span data-ttu-id="6de29-363">您也可以參考 [Azure 備份相關的常見問題集](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6de29-363">You can also refer to [Azure Backup related FAQs](backup-azure-backup-faq.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6de29-364">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6de29-364">Next steps</span></span>
<span data-ttu-id="6de29-365">您可以在 Microsoft TechNet 網站上取得有關 [準備 DPM 的環境](https://technet.microsoft.com/library/hh758176.aspx) 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6de29-365">You can get detailed information about [preparing your environment for DPM](https://technet.microsoft.com/library/hh758176.aspx) on the Microsoft TechNet site.</span></span> <span data-ttu-id="6de29-366">其中也包含可據以部署和使用 Azure 備份伺服器之支援組態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6de29-366">It also contains information about supported configurations on which Azure Backup Server can be deployed and used.</span></span>

<span data-ttu-id="6de29-367">請參閱這些文章，以深入了解使用 Microsoft Azure 備份伺服器來保護工作負載。</span><span class="sxs-lookup"><span data-stu-id="6de29-367">You can use these articles to gain a deeper understanding of workload protection using Microsoft Azure Backup server.</span></span>

* [<span data-ttu-id="6de29-368">SQL Server 備份</span><span class="sxs-lookup"><span data-stu-id="6de29-368">SQL Server backup</span></span>](backup-azure-backup-sql.md)
* [<span data-ttu-id="6de29-369">SharePoint 伺服器備份</span><span class="sxs-lookup"><span data-stu-id="6de29-369">SharePoint server backup</span></span>](backup-azure-backup-sharepoint.md)
* [<span data-ttu-id="6de29-370">替代伺服器備份</span><span class="sxs-lookup"><span data-stu-id="6de29-370">Alternate server backup</span></span>](backup-azure-alternate-dpm-server.md)
