---
title: "VMware VM 複寫至 Azure (CSP 計劃) 的多租用戶支援 | Microsoft Docs"
description: "描述如何使用 Azure 入口網站在多租用戶環境中部署 Azure Site Recovery，以透過 CSP 計畫協調內部部署 VMware 虛擬機器 (VM) 至 Azure 的複寫、容錯移轉和復原"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 97edbe67c25036dc1156f0f0ca5431a617d7a004
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-to-azure-through-csp"></a><span data-ttu-id="dc163-103">Azure Site Recovery 中的多租用戶支援，適用於透過 CSP 將 VMware 虛擬機器複寫到 Azure</span><span class="sxs-lookup"><span data-stu-id="dc163-103">Multi-tenant support in Azure Site Recovery for replicating VMware virtual machines to Azure through CSP</span></span>

<span data-ttu-id="dc163-104">Azure Site Recovery 支援租用戶訂用帳戶的多租用戶環境。</span><span class="sxs-lookup"><span data-stu-id="dc163-104">Azure Site Recovery supports multi-tenant environments for tenant subscriptions.</span></span> <span data-ttu-id="dc163-105">對於透過 Microsoft Cloud 解決方案提供者 (CSP) 方案建立及管理的租用戶訂用帳戶，它也支援多租用戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-105">It also supports multi-tenancy for tenant subscriptions that are created and managed through the Microsoft Cloud Solution Provider (CSP) program.</span></span> <span data-ttu-id="dc163-106">本文中詳述實作及管理多租用戶 VMware 到 Azure 案例的指南。</span><span class="sxs-lookup"><span data-stu-id="dc163-106">This article details the guidance for implementing and managing multi-tenant VMware-to-Azure scenarios.</span></span> <span data-ttu-id="dc163-107">其中也涵蓋透過 CSP 建立及管理租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-107">It also covers creating and managing tenant subscriptions through CSP.</span></span>

<span data-ttu-id="dc163-108">本指南與複寫 VMware 虛擬機器到 Azure 的現有文件密切相關。</span><span class="sxs-lookup"><span data-stu-id="dc163-108">This guidance draws heavily from the existing documentation for replicating VMware virtual machines to Azure.</span></span> <span data-ttu-id="dc163-109">如需詳細資訊，請參閱[使用 Site Recovery 將 VMware 虛擬機器複寫至 Azure](site-recovery-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="dc163-109">For more information, see [Replicate VMware virtual machines to Azure with Site Recovery](site-recovery-vmware-to-azure.md).</span></span>

## <a name="multi-tenant-environments"></a><span data-ttu-id="dc163-110">多租用戶環境</span><span class="sxs-lookup"><span data-stu-id="dc163-110">Multi-tenant environments</span></span>
<span data-ttu-id="dc163-111">多租用戶模型主要有三種：</span><span class="sxs-lookup"><span data-stu-id="dc163-111">There are three major multi-tenant models:</span></span>

* <span data-ttu-id="dc163-112">**共用主機服務提供者 (HSP)**：合作夥伴擁有實體基礎結構，而使用者則共用資源 (如 vCenter、資料中心、實體儲存體等) 以將多租用戶的虛擬機器裝載在同一個基礎結構。</span><span class="sxs-lookup"><span data-stu-id="dc163-112">**Shared Hosting Services Provider (HSP)**: The partner owns the physical infrastructure and uses shared resources (vCenter, datacenters, physical storage, and so on) to host multiple tenants’ VMs on the same infrastructure.</span></span> <span data-ttu-id="dc163-113">合作夥伴可提供災害復原管理做為受管理的服務，租用戶也可以擁有災害復原做為自助服務方案。</span><span class="sxs-lookup"><span data-stu-id="dc163-113">The partner can provide disaster-recovery management as a managed service, or the tenant can own disaster recovery as a self-service solution.</span></span>

* <span data-ttu-id="dc163-114">**專用主機服務提供者**：合作夥伴擁有實體基礎結構，但使用專用資源 (如多個 vCenters、實體資料存放區等) 在個別的基礎結構上裝載每個租用戶的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dc163-114">**Dedicated Hosting Services Provider**: The partner owns the physical infrastructure but uses dedicated resources (multiple vCenters, physical datastores, and so on) to host each tenant’s VMs on a separate infrastructure.</span></span> <span data-ttu-id="dc163-115">合作夥伴可提供災害復原管理做為受管理的服務，租用戶也可以擁有災害復原做為自助服務方案。</span><span class="sxs-lookup"><span data-stu-id="dc163-115">The partner can provide disaster-recovery management as a managed service, or the tenant can own it as a self-service solution.</span></span>

* <span data-ttu-id="dc163-116">**受管理的服務提供者 (MSP)** – 客戶擁有裝載虛擬機器的實體基礎結構，而合作夥伴則提供災害復原支援及管理。</span><span class="sxs-lookup"><span data-stu-id="dc163-116">**Managed Services Provider (MSP)**: The customer owns the physical infrastructure that hosts the VMs, and the partner provides disaster-recovery enablement and management.</span></span>

## <a name="shared-hosting-multi-tenant-guidance"></a><span data-ttu-id="dc163-117">共用主機多租用戶指南</span><span class="sxs-lookup"><span data-stu-id="dc163-117">Shared-hosting multi-tenant guidance</span></span>
<span data-ttu-id="dc163-118">本節詳述共用主機案例。</span><span class="sxs-lookup"><span data-stu-id="dc163-118">This section covers the shared-hosting scenario in detail.</span></span> <span data-ttu-id="dc163-119">另外兩個案例是共用主機案例的子集，且使用相同的原則。</span><span class="sxs-lookup"><span data-stu-id="dc163-119">The other two scenarios are subsets of the shared-hosting scenario, and they use the same principles.</span></span> <span data-ttu-id="dc163-120">共用主機指南最後面會詳述其中的差異。</span><span class="sxs-lookup"><span data-stu-id="dc163-120">The differences are described at the end of the shared-hosting guidance.</span></span>

<span data-ttu-id="dc163-121">多租用戶案例的基本需求是隔離不同的租用戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-121">The basic requirement in a multi-tenant scenario is to isolate the various tenants.</span></span> <span data-ttu-id="dc163-122">一個租用戶無法觀察另一個租用戶裝載的內容。</span><span class="sxs-lookup"><span data-stu-id="dc163-122">One tenant should not be able to observe what another tenant has hosted.</span></span> <span data-ttu-id="dc163-123">這個需求在自助管理環境中，比在合作夥伴管理的環境中來得重要，甚至有重大影響。</span><span class="sxs-lookup"><span data-stu-id="dc163-123">In a partner-managed environment, this requirement is not as important as it is in a self-service environment, where it can be critical.</span></span> <span data-ttu-id="dc163-124">本指南假設租用戶隔離是必要條件。</span><span class="sxs-lookup"><span data-stu-id="dc163-124">This guidance assumes that tenant isolation is required.</span></span>

<span data-ttu-id="dc163-125">下圖說明這個架構：</span><span class="sxs-lookup"><span data-stu-id="dc163-125">The architecture is presented in the following diagram:</span></span>

<span data-ttu-id="dc163-126">![含一個 vCenter 的共用 HSP](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)</span><span class="sxs-lookup"><span data-stu-id="dc163-126">![Shared HSP with one vCenter](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)</span></span>  
<span data-ttu-id="dc163-127">**含一個 vCenter 的共用主機案例**</span><span class="sxs-lookup"><span data-stu-id="dc163-127">**Shared-hosting scenario with one vCenter**</span></span>

<span data-ttu-id="dc163-128">如上圖所示，每個客戶都有個別的管理伺服器。</span><span class="sxs-lookup"><span data-stu-id="dc163-128">As seen in the preceding diagram, each customer has a separate management server.</span></span> <span data-ttu-id="dc163-129">這個設定可以將租用戶限制於只能存取租用戶特定虛擬機器，以達到租用戶隔離的目的。</span><span class="sxs-lookup"><span data-stu-id="dc163-129">This configuration limits tenant access to tenant-specific VMs and enables tenant isolation.</span></span> <span data-ttu-id="dc163-130">VMware 虛擬機器複寫案例會使用組態伺服器來管理帳戶以探索虛擬機器及安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="dc163-130">A VMware virtual-machine replication scenario uses the configuration server to manage accounts to discover VMs and install agents.</span></span> <span data-ttu-id="dc163-131">我們會針對多租用戶環境遵循相同的原則，但是另外透過 vCenter 存取控制來限制 VM 探索。</span><span class="sxs-lookup"><span data-stu-id="dc163-131">We follow the same principles for multi-tenant environments, with the addition of restricting VM discovery through vCenter access control.</span></span>

<span data-ttu-id="dc163-132">資料隔離的需求會使得基礎結構機密資訊 (如存取認證) 對租用戶保持公開。</span><span class="sxs-lookup"><span data-stu-id="dc163-132">The data-isolation requirement necessitates that all sensitive infrastructure information (such as access credentials) remain undisclosed to tenants.</span></span> <span data-ttu-id="dc163-133">基於這個理由，建議所有管理伺服器的元件都維持在合作夥伴的獨佔控制之下。</span><span class="sxs-lookup"><span data-stu-id="dc163-133">For this reason, we recommend that all components of the management server remain under the exclusive control of the partner.</span></span> <span data-ttu-id="dc163-134">管理伺服器元件包括：</span><span class="sxs-lookup"><span data-stu-id="dc163-134">The management server components are:</span></span>
* <span data-ttu-id="dc163-135">組態伺服器 (CS)</span><span class="sxs-lookup"><span data-stu-id="dc163-135">Configuration server (CS)</span></span>
* <span data-ttu-id="dc163-136">處理序伺服器 (PS)</span><span class="sxs-lookup"><span data-stu-id="dc163-136">Process server (PS)</span></span>
* <span data-ttu-id="dc163-137">主要目標伺服器 (MT)</span><span class="sxs-lookup"><span data-stu-id="dc163-137">Master target server (MT)</span></span> 

<span data-ttu-id="dc163-138">向外延展 PS 也是在合作夥伴的控制之下。</span><span class="sxs-lookup"><span data-stu-id="dc163-138">A scale-out PS is also under the partner's control.</span></span>

### <a name="every-cs-in-the-multi-tenant-scenario-uses-two-accounts"></a><span data-ttu-id="dc163-139">多租用戶案例中的每個 CS 都使用兩個帳戶</span><span class="sxs-lookup"><span data-stu-id="dc163-139">Every CS in the multi-tenant scenario uses two accounts</span></span>

- <span data-ttu-id="dc163-140">**vCenter 存取帳戶**：此帳戶可用來探索租用戶虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dc163-140">**vCenter access account**: Use this account to discover tenant VMs.</span></span> <span data-ttu-id="dc163-141">帳戶有獲得指派的 vCenter 存取權限 (如下一節所述)。</span><span class="sxs-lookup"><span data-stu-id="dc163-141">It has vCenter access permissions assigned to it (as described in the next section).</span></span> <span data-ttu-id="dc163-142">為了避免意外的存取權限洩漏，建議夥伴自行在設定工具中輸入這些認證。</span><span class="sxs-lookup"><span data-stu-id="dc163-142">To help avoid accidental access leaks, we recommend that partners enter these credentials themselves in the configuration tool.</span></span>

- <span data-ttu-id="dc163-143">**虛擬機器存取帳戶**：此帳戶是用來在租用戶上，透過自動推送安裝行動代理程式。</span><span class="sxs-lookup"><span data-stu-id="dc163-143">**Virtual machine access account**: Use this account to install the mobility agent on the tenant VMs through an automatic push.</span></span> <span data-ttu-id="dc163-144">這通常是租用戶可能會提供給合作夥伴的網域帳戶，或可能由合作夥伴直接管理的網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-144">It is usually a domain account that a tenant might provide to a partner or that, alternatively, the partner might manage directly.</span></span> <span data-ttu-id="dc163-145">如果租用戶不要直接與合作夥伴分享詳細資料，租用戶可以透過限時的 CS 存取權來輸入認證，也可以在合作夥伴的協助下手動安裝行動代理程式。</span><span class="sxs-lookup"><span data-stu-id="dc163-145">If a tenant doesn't want to share the details with the partner directly, he or she can be allowed to enter the credentials through limited-time access to the CS or, with the partner's assistance, install mobility agents manually.</span></span>

### <a name="requirements-for-a-vcenter-access-account"></a><span data-ttu-id="dc163-146">vCenter 存取帳戶的需求</span><span class="sxs-lookup"><span data-stu-id="dc163-146">Requirements for a vCenter access account</span></span>

<span data-ttu-id="dc163-147">如前一節所述，您必須使用獲指派特殊角色的帳戶設定 CS。</span><span class="sxs-lookup"><span data-stu-id="dc163-147">As mentioned in the preceding section, you must configure the CS with an account that has a special role assigned to it.</span></span> <span data-ttu-id="dc163-148">針對每個 vCenter 物件，必須將角色指派套用於 vCenter 存取帳戶，而且不要傳播到子物件。</span><span class="sxs-lookup"><span data-stu-id="dc163-148">The role assignment must be applied to the vCenter access account for each vCenter object and not propagated to the child objects.</span></span> <span data-ttu-id="dc163-149">此設定可以確保租用戶隔離，因為存取傳播可能會導致意外存取其他物件。</span><span class="sxs-lookup"><span data-stu-id="dc163-149">This configuration ensures tenant isolation, because access propagation can result in accidental access to other objects.</span></span>

![傳播到子物件選項](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

<span data-ttu-id="dc163-151">替代方案是在資料中心物件指派使用者帳戶和角色，並將這些傳播到子物件。</span><span class="sxs-lookup"><span data-stu-id="dc163-151">The alternative is to assign the user account and role at the datacenter object and propagate them to the child objects.</span></span> <span data-ttu-id="dc163-152">然後將每個物件 (例如其他租用戶的虛擬機器) 的*無存取*角色授與應該無法存取特定租用戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-152">Then give the account a *No access* role for every object (such as other tenants’ VMs) that should be inaccessible to a particular tenant.</span></span> <span data-ttu-id="dc163-153">這個設定相當繁瑣，而且會意外公開存取控制，因為會對每個新的子物件自動授與從父物件繼承的存取權。</span><span class="sxs-lookup"><span data-stu-id="dc163-153">This configuration is cumbersome, and it exposes accidental access controls, because every new child object is also automatically granted access that's inherited from the parent.</span></span> <span data-ttu-id="dc163-154">因此建議採用第一種方法。</span><span class="sxs-lookup"><span data-stu-id="dc163-154">Therefore, we recommend that you use the first approach.</span></span>

<span data-ttu-id="dc163-155">vCenter 帳戶存取程序如下：</span><span class="sxs-lookup"><span data-stu-id="dc163-155">The vCenter account-access procedure is as follows:</span></span>

1. <span data-ttu-id="dc163-156">藉由複製預先定義的「唯讀」角色來建立新的角色，並以易記名稱 (例如此範例中顯示的 Azure_Site_Recovery) 命名。</span><span class="sxs-lookup"><span data-stu-id="dc163-156">Create a new role by cloning the pre-defined *Read-only* role, and then give it a convenient name (such as Azure_Site_Recovery, as shown in this example).</span></span>

2. <span data-ttu-id="dc163-157">將下列權限指派給這個角色：</span><span class="sxs-lookup"><span data-stu-id="dc163-157">Assign the following permissions to this role:</span></span>

    * <span data-ttu-id="dc163-158">**資料存放區**：配置空間、瀏覽資料存放區、底層檔案作業、移除檔案、更新虛擬機器檔案</span><span class="sxs-lookup"><span data-stu-id="dc163-158">**Datastore**: Allocate space, Browse datastore, Low-level file operations, Remove file, Update virtual machine files</span></span>

    * <span data-ttu-id="dc163-159">**網路**：網路指派</span><span class="sxs-lookup"><span data-stu-id="dc163-159">**Network**: Network assign</span></span>

    * <span data-ttu-id="dc163-160">**資源**：指派虛擬機器至資源集區、移轉已關閉電源的虛擬機器、移轉已開啟電源的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="dc163-160">**Resource**: Assign VM to resource pool, Migrate powered off VM, Migrate powered on VM</span></span>

    * <span data-ttu-id="dc163-161">**工作**：建立工作、更新工作</span><span class="sxs-lookup"><span data-stu-id="dc163-161">**Tasks**: Create task, Update task</span></span>

    * <span data-ttu-id="dc163-162">**虛擬機器**：</span><span class="sxs-lookup"><span data-stu-id="dc163-162">**Virtual machine**:</span></span> 
        * <span data-ttu-id="dc163-163">組態 > 全部</span><span class="sxs-lookup"><span data-stu-id="dc163-163">Configuration > all</span></span>
        * <span data-ttu-id="dc163-164">互動 > 回答問題、裝置連線、設定 CD 媒體、設定磁碟片媒體、電源關閉、電源開啟、VMware 工具安裝</span><span class="sxs-lookup"><span data-stu-id="dc163-164">Interaction > Answer question, Device connection, Configure CD media, Configure floppy media, Power off, Power on, VMware tools install</span></span>
        * <span data-ttu-id="dc163-165">清查 > 從現有建立、建立新的、註冊、取消註冊</span><span class="sxs-lookup"><span data-stu-id="dc163-165">Inventory > Create from existing, Create new, Register, Unregister</span></span>
        * <span data-ttu-id="dc163-166">佈建 > 允許虛擬機器下載、允許虛擬機器檔案上傳</span><span class="sxs-lookup"><span data-stu-id="dc163-166">Provisioning > Allow virtual machine download, Allow virtual machine files upload</span></span>
        * <span data-ttu-id="dc163-167">快照集管理 > 移除快照集</span><span class="sxs-lookup"><span data-stu-id="dc163-167">Snapshot management > Remove snapshots</span></span>

    ![[編輯角色] 對話方塊](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. <span data-ttu-id="dc163-169">針對不同物件，指派存取層級給 vCenter 帳戶 (在租用戶 CS 中使用)：</span><span class="sxs-lookup"><span data-stu-id="dc163-169">Assign access levels to the vCenter account (used in the tenant CS) for various objects, as follows:</span></span>

>| <span data-ttu-id="dc163-170">Object</span><span class="sxs-lookup"><span data-stu-id="dc163-170">Object</span></span> | <span data-ttu-id="dc163-171">角色</span><span class="sxs-lookup"><span data-stu-id="dc163-171">Role</span></span> | <span data-ttu-id="dc163-172">備註</span><span class="sxs-lookup"><span data-stu-id="dc163-172">Remarks</span></span> |
>| --- | --- | --- |
>| <span data-ttu-id="dc163-173">vCenter</span><span class="sxs-lookup"><span data-stu-id="dc163-173">vCenter</span></span> | <span data-ttu-id="dc163-174">唯讀</span><span class="sxs-lookup"><span data-stu-id="dc163-174">Read-Only</span></span> | <span data-ttu-id="dc163-175">只用以允許 vCenter 存取以管理其他物件。</span><span class="sxs-lookup"><span data-stu-id="dc163-175">Needed only to allow vCenter access for managing different objects.</span></span> <span data-ttu-id="dc163-176">如果帳戶不會提供給租用戶，或用於任何 vCenter 上的管理作業，則可以移除此權限。</span><span class="sxs-lookup"><span data-stu-id="dc163-176">You can remove this permission if the account is never going to be provided to a tenant or used for any management operations on the vCenter.</span></span> |
>| <span data-ttu-id="dc163-177">資料中心</span><span class="sxs-lookup"><span data-stu-id="dc163-177">Datacenter</span></span> | <span data-ttu-id="dc163-178">Azure_Site_Recovery</span><span class="sxs-lookup"><span data-stu-id="dc163-178">Azure_Site_Recovery</span></span> |  |
>| <span data-ttu-id="dc163-179">主機和主機叢集</span><span class="sxs-lookup"><span data-stu-id="dc163-179">Host and host cluster</span></span> | <span data-ttu-id="dc163-180">Azure_Site_Recovery</span><span class="sxs-lookup"><span data-stu-id="dc163-180">Azure_Site_Recovery</span></span> | <span data-ttu-id="dc163-181">再次確認存取權在物件層級，以限制只有可存取的主機在容錯移轉前和容錯回復後有租用戶虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dc163-181">Re-ensures that access is at the object level, so that only accessible hosts have tenant VMs before failover and after failback.</span></span> |
>| <span data-ttu-id="dc163-182">資料存放區和資料存放區叢集</span><span class="sxs-lookup"><span data-stu-id="dc163-182">Datastore and datastore cluster</span></span> | <span data-ttu-id="dc163-183">Azure_Site_Recovery</span><span class="sxs-lookup"><span data-stu-id="dc163-183">Azure_Site_Recovery</span></span> | <span data-ttu-id="dc163-184">同上。</span><span class="sxs-lookup"><span data-stu-id="dc163-184">Same as preceding.</span></span> |
>| <span data-ttu-id="dc163-185">網路</span><span class="sxs-lookup"><span data-stu-id="dc163-185">Network</span></span> | <span data-ttu-id="dc163-186">Azure_Site_Recovery</span><span class="sxs-lookup"><span data-stu-id="dc163-186">Azure_Site_Recovery</span></span> |  |
>| <span data-ttu-id="dc163-187">管理伺服器</span><span class="sxs-lookup"><span data-stu-id="dc163-187">Management server</span></span> | <span data-ttu-id="dc163-188">Azure_Site_Recovery</span><span class="sxs-lookup"><span data-stu-id="dc163-188">Azure_Site_Recovery</span></span> | <span data-ttu-id="dc163-189">如果有任何元件在 CS 機器以外，包括所有元件 (CS、PS 及 MT) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="dc163-189">Includes access to all components (CS, PS, and MT) if any are outside the CS machine.</span></span> |
>| <span data-ttu-id="dc163-190">租用戶 VM</span><span class="sxs-lookup"><span data-stu-id="dc163-190">Tenant VMs</span></span> | <span data-ttu-id="dc163-191">Azure_Site_Recovery</span><span class="sxs-lookup"><span data-stu-id="dc163-191">Azure_Site_Recovery</span></span> | <span data-ttu-id="dc163-192">確保特定租用戶的任何新租用戶虛擬機器也會有此存取權，否則將無法透過 Azure 入口網站探索它們。</span><span class="sxs-lookup"><span data-stu-id="dc163-192">Ensures that any new tenant VMs of a particular tenant also get this access, or they will not be discoverable through the Azure portal.</span></span> |

<span data-ttu-id="dc163-193">現在已經完成 vCenter 帳戶存取權。</span><span class="sxs-lookup"><span data-stu-id="dc163-193">The vCenter account access is now complete.</span></span> <span data-ttu-id="dc163-194">這個步驟可以滿足完成容錯回復作業的最小權限需求。</span><span class="sxs-lookup"><span data-stu-id="dc163-194">This step fulfills the minimum permissions requirement to complete failback operations.</span></span> <span data-ttu-id="dc163-195">也可以搭配現有的原則使用這些存取權限。</span><span class="sxs-lookup"><span data-stu-id="dc163-195">You can also use these access permissions with your existing policies.</span></span> <span data-ttu-id="dc163-196">只要將現有的權限集修改成包含上面步驟 2 詳述的角色權限即可。</span><span class="sxs-lookup"><span data-stu-id="dc163-196">Just modify your existing permissions set to include role permissions from step 2, detailed previously.</span></span>

<span data-ttu-id="dc163-197">若要限制災害復原作業僅進行到容錯移轉狀態，而沒有容錯回復的功能，請遵循上述程序，但是不要指派 *Azure_Site_Recovery*給 vCenter 存取帳戶，而是改為只指派*唯讀*角色。</span><span class="sxs-lookup"><span data-stu-id="dc163-197">To restrict disaster-recovery operations until the failover state (that is, without failback capabilities), follow the preceding  procedure, with an exception: instead of assigning the *Azure_Site_Recovery* role to the vCenter access account, assign only a *Read-Only* role to that account.</span></span> <span data-ttu-id="dc163-198">這個權限集合會允許虛擬機器複寫和容錯移轉，而不允許容錯回復。</span><span class="sxs-lookup"><span data-stu-id="dc163-198">This permission set allows VM replication and failover, and it does not allow failback.</span></span> <span data-ttu-id="dc163-199">以上程序的其餘部分都保持原狀。</span><span class="sxs-lookup"><span data-stu-id="dc163-199">Everything else in the preceding process remains as is.</span></span> <span data-ttu-id="dc163-200">為了確保租用戶隔離及限制虛擬機器探索，所有權限仍僅指派到物件層級而未傳播到子物件。</span><span class="sxs-lookup"><span data-stu-id="dc163-200">To ensure tenant isolation and restrict VM discovery, every permission is still assigned at the object level only and not propagated to child objects.</span></span>

## <a name="other-multi-tenant-environments"></a><span data-ttu-id="dc163-201">其他多租用戶環境</span><span class="sxs-lookup"><span data-stu-id="dc163-201">Other multi-tenant environments</span></span>

<span data-ttu-id="dc163-202">上節描述如何針對共用主機解決方案設定多租用戶環境。</span><span class="sxs-lookup"><span data-stu-id="dc163-202">The preceding section described how to set up a multi-tenant environment for a shared hosting solution.</span></span> <span data-ttu-id="dc163-203">另外兩個主要解決方案是專用主機和受管理的服務。</span><span class="sxs-lookup"><span data-stu-id="dc163-203">The other two major solutions are dedicated hosting and managed service.</span></span> <span data-ttu-id="dc163-204">下列各節將說明這些解決方案的架構。</span><span class="sxs-lookup"><span data-stu-id="dc163-204">The architecture for these solutions is described in the following sections.</span></span>

### <a name="dedicated-hosting-solution"></a><span data-ttu-id="dc163-205">專用主機解決方案</span><span class="sxs-lookup"><span data-stu-id="dc163-205">Dedicated hosting solution</span></span>

<span data-ttu-id="dc163-206">如下圖所示，專用主機方案的架構差異是每個租用戶的基礎結構完全針對該租用戶設定。</span><span class="sxs-lookup"><span data-stu-id="dc163-206">As shown in the following diagram, the architectural difference in a dedicated hosting solution is that each tenant’s infrastructure is set up for that tenant only.</span></span> <span data-ttu-id="dc163-207">因為租用戶是透過個別的 vCenter 隔離，所以主機提供者仍必須按照針對共用主機提供的 CSP 步驟來執行，但不需要擔心租用戶隔離。</span><span class="sxs-lookup"><span data-stu-id="dc163-207">Because tenants are isolated through separate vCenters, the hosting provider must still follow the CSP steps provided for shared hosting but does not need to worry about tenant isolation.</span></span> <span data-ttu-id="dc163-208">CSP 安裝程式會保持不變。</span><span class="sxs-lookup"><span data-stu-id="dc163-208">CSP setup remains unchanged.</span></span>

<span data-ttu-id="dc163-209">![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)</span><span class="sxs-lookup"><span data-stu-id="dc163-209">![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)</span></span>  
<span data-ttu-id="dc163-210">**含多個 vCenters 的專用主機案例**</span><span class="sxs-lookup"><span data-stu-id="dc163-210">**Dedicated hosting scenario with multiple vCenters**</span></span>

### <a name="managed-service-solution"></a><span data-ttu-id="dc163-211">受管理的服務解決方案</span><span class="sxs-lookup"><span data-stu-id="dc163-211">Managed service solution</span></span>

<span data-ttu-id="dc163-212">如下圖所示，受管理的服務方案本身的架構差異是每個租用戶的基礎結構在實體上與其他租用戶的基礎結構分開。</span><span class="sxs-lookup"><span data-stu-id="dc163-212">As shown in the following diagram, the architectural difference in a managed service solution is that each tenant’s infrastructure is also physically separate from other tenants' infrastructure.</span></span> <span data-ttu-id="dc163-213">此案例通常是在租用戶擁有基礎結構時存在，而且需要解決方案提供者來管理災害復原。</span><span class="sxs-lookup"><span data-stu-id="dc163-213">This scenario usually exists when the tenant owns the infrastructure and wants a solution provider to manage disaster recovery.</span></span> <span data-ttu-id="dc163-214">同樣地，因為租用戶在實體上透過不同的基礎結構來隔離，所以合作夥伴仍需要按照針對共用主機提供的 CSP 步驟來執行，但不需要擔心租用戶隔離。</span><span class="sxs-lookup"><span data-stu-id="dc163-214">Again, because tenants are physically isolated through different infrastructures, the partner needs to follow the CSP steps provided for shared hosting but does not need to worry about tenant isolation.</span></span> <span data-ttu-id="dc163-215">CSP 佈建保持不變。</span><span class="sxs-lookup"><span data-stu-id="dc163-215">CSP provisioning remains unchanged.</span></span>

<span data-ttu-id="dc163-216">![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)</span><span class="sxs-lookup"><span data-stu-id="dc163-216">![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)</span></span>  
<span data-ttu-id="dc163-217">**含多個 vCenters 的受管理的服務案例**</span><span class="sxs-lookup"><span data-stu-id="dc163-217">**Managed service scenario with multiple vCenters**</span></span>

## <a name="csp-program-overview"></a><span data-ttu-id="dc163-218">CSP 計畫概觀</span><span class="sxs-lookup"><span data-stu-id="dc163-218">CSP program overview</span></span>
<span data-ttu-id="dc163-219">[CSP 計畫](https://partner.microsoft.com/en-US/cloud-solution-provider)致力於和合作夥伴合作提供所有 Microsoft 雲端服務 (包括 Office 365、Enterprise Mobility Suite 和 Microsoft Azure) 以達到雙贏。</span><span class="sxs-lookup"><span data-stu-id="dc163-219">The [CSP program](https://partner.microsoft.com/en-US/cloud-solution-provider) fosters better-together stories that offer partners all Microsoft cloud services, including Office 365, Enterprise Mobility Suite, and Microsoft Azure.</span></span> <span data-ttu-id="dc163-220">藉由 CSP，我們的合作夥伴全面掌握與客戶的端對端關係，並且成為主要的關係連絡窗口。</span><span class="sxs-lookup"><span data-stu-id="dc163-220">With CSP, our partners own the end-to-end relationship with customers and become the primary relationship contact point.</span></span> <span data-ttu-id="dc163-221">合作夥伴可以為客戶部署 Azure 訂用帳戶，並將這些訂用帳戶與他們自己的加值自訂優惠結合。</span><span class="sxs-lookup"><span data-stu-id="dc163-221">Partners can deploy Azure subscriptions for customers and combine the subscriptions with their own value-added, customized offerings.</span></span>

<span data-ttu-id="dc163-222">藉由 Azure Site Recovery，合作夥伴可以直接透過 CSP 管理客戶的完整災害復原解決方案。</span><span class="sxs-lookup"><span data-stu-id="dc163-222">With Azure Site Recovery, partners can manage the complete Disaster Recovery solution for customers directly through CSP.</span></span> <span data-ttu-id="dc163-223">或者，也可以使用 CSP 設定 Site Recovery 環境，並讓客戶藉由自助服務的方式管理自己的災害復原需求。</span><span class="sxs-lookup"><span data-stu-id="dc163-223">Or they can use CSP to set up Site Recovery environments and let customers manage their own disaster-recovery needs in a self-service manner.</span></span> <span data-ttu-id="dc163-224">在這兩種情況下，合作夥伴是 Site Recovery 與客戶之間的連絡窗口。</span><span class="sxs-lookup"><span data-stu-id="dc163-224">In both scenarios, partners are the liaison between Site Recovery and their customers.</span></span> <span data-ttu-id="dc163-225">合作夥伴負責維護客戶關係，以及向客戶收取 Site Recovery 使用量的費用。</span><span class="sxs-lookup"><span data-stu-id="dc163-225">Partners service the customer relationship and bill customers for Site Recovery usage.</span></span>

## <a name="create-and-manage-tenant-accounts"></a><span data-ttu-id="dc163-226">建立及管理租用戶帳戶</span><span class="sxs-lookup"><span data-stu-id="dc163-226">Create and manage tenant accounts</span></span>

### <a name="step-0-prerequisite-check"></a><span data-ttu-id="dc163-227">步驟 0：必要條件檢查</span><span class="sxs-lookup"><span data-stu-id="dc163-227">Step 0: Prerequisite check</span></span>

<span data-ttu-id="dc163-228">虛擬機器的必要條件和 [Azure Site Recovery 文件](site-recovery-vmware-to-azure.md)中所述相同。</span><span class="sxs-lookup"><span data-stu-id="dc163-228">The VM prerequisites are the same as described in the [Azure Site Recovery documentation](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="dc163-229">除了這些必要條件之外，也應該要先設定好上述存取控制，才能透過 CSP 進行租用戶管理。</span><span class="sxs-lookup"><span data-stu-id="dc163-229">In addition to those prerequisites, you should have the previously mentioned access controls in place before you proceed with tenant management through CSP.</span></span> <span data-ttu-id="dc163-230">針對每個租用戶建立可以和租用戶虛擬機器及合作夥伴的 vCenter 通訊的個別「管理伺服器」。</span><span class="sxs-lookup"><span data-stu-id="dc163-230">For each tenant, create a separate management server that can communicate with the tenant VMs and partner’s vCenter.</span></span> <span data-ttu-id="dc163-231">只有合作夥伴有此伺服器的存取權限。</span><span class="sxs-lookup"><span data-stu-id="dc163-231">Only the partner has access rights to this server.</span></span>

### <a name="step-1-create-a-tenant-account"></a><span data-ttu-id="dc163-232">步驟 1︰建立租用戶帳戶</span><span class="sxs-lookup"><span data-stu-id="dc163-232">Step 1: Create a tenant account</span></span>

1. <span data-ttu-id="dc163-233">透過 [Microsoft 合作夥伴中心](https://partnercenter.microsoft.com/) 登入 CSP 帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-233">Through [Microsoft Partner Center](https://partnercenter.microsoft.com/), sign in to your CSP account.</span></span> 
 
2. <span data-ttu-id="dc163-234">在 [儀表板] 功能表上，選取 [客戶]。</span><span class="sxs-lookup"><span data-stu-id="dc163-234">On the **Dashboard** menu, select **Customers**.</span></span>

    ![Microsoft 夥伴中心客戶連結](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. <span data-ttu-id="dc163-236">在開啟的頁面上，按一下 [新增客戶] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc163-236">On the page that opens, click the **Add customer** button.</span></span>

    ![[新增客戶] 按鈕](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. <span data-ttu-id="dc163-238">在 [新客戶] 頁面上，填入租用戶的所有帳戶資訊詳細資料，然後按一下 [下一步: 訂閱]。</span><span class="sxs-lookup"><span data-stu-id="dc163-238">On the **New Customer** page, fill in the account information details for the tenant, and then click **Next: Subscriptions**.</span></span>

    ![[帳戶資訊] 頁面](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. <span data-ttu-id="dc163-240">在訂閱選取頁面上，勾選 [Microsoft Azure] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="dc163-240">On the subscriptions selection page, select the **Microsoft Azure** check box.</span></span> <span data-ttu-id="dc163-241">您可以立即或在其他任何時候新增其他訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-241">You can add other subscriptions now or at any other time.</span></span>

    ![[Microsoft Azure 訂用帳戶] 核取方塊](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. <span data-ttu-id="dc163-243">在 [檢閱] 頁面上，確認租用戶詳細資料，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="dc163-243">On the **Review** page, confirm the tenant details, and then click **Submit**.</span></span>

    ![[檢閱] 頁面](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    <span data-ttu-id="dc163-245">您建立租用戶帳戶後，確認網頁隨即出現，顯示預設帳戶的詳細資料和該訂用帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="dc163-245">After you've created the tenant account, a confirmation page appears, displaying the details of the default account and the password for that subscription.</span></span> 

7. <span data-ttu-id="dc163-246">儲存資訊並在稍後視需要透過 Azure 入口網站登入網頁來變更密碼。</span><span class="sxs-lookup"><span data-stu-id="dc163-246">Save the information, and change the password later as necessary through the Azure portal sign-in page.</span></span>  
 
    <span data-ttu-id="dc163-247">您可以與租用戶共用這些既有的資訊，也可以視需要建立和共用不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-247">You can share this information with the tenant as is, or you can create and share a separate account if necessary.</span></span>

### <a name="step-2-access-the-tenant-account"></a><span data-ttu-id="dc163-248">步驟 2︰存取租用戶帳戶</span><span class="sxs-lookup"><span data-stu-id="dc163-248">Step 2: Access the tenant account</span></span>

<span data-ttu-id="dc163-249">如「步驟 1：建立租用戶帳戶」所述，您可以透過 Microsoft 夥伴中心儀表板存取租用戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-249">You can access the tenant’s subscription through the Microsoft Partner Center Dashboard, as described in "Step 1: Create a tenant account."</span></span> 

1. <span data-ttu-id="dc163-250">移至 [客戶] 頁面，然後按一下租用戶帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="dc163-250">Go to the **Customers** page, and then click the name of the tenant account.</span></span>

2. <span data-ttu-id="dc163-251">在租用戶帳戶的 [訂用帳戶] 頁面上，您可以監視現有帳戶的訂用帳戶，並且視需要新增更多訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-251">On the **Subscriptions** page of the tenant account, you can monitor the existing account subscriptions and add more subscriptions, as required.</span></span> <span data-ttu-id="dc163-252">若要管理租用戶的災復原作業，請選取 [所有資源 (Azure 入口網站)]。</span><span class="sxs-lookup"><span data-stu-id="dc163-252">To manage the tenant’s disaster-recovery operations, select **All resources (Azure portal)**.</span></span>

    ![[所有資源] 連結](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    <span data-ttu-id="dc163-254">按一下 [所有資源] 將授與租用戶的 Azure 訂用帳戶存取權限。</span><span class="sxs-lookup"><span data-stu-id="dc163-254">Clicking **All resources** grants you access to the tenant’s Azure subscriptions.</span></span> <span data-ttu-id="dc163-255">您可以按一下 Azure 入口網站右上方的 [Azure Active Directory] 連結，以確認存取權限。</span><span class="sxs-lookup"><span data-stu-id="dc163-255">You can verify access by clicking the Azure Active Directory link at the top right of the Azure portal.</span></span>

    ![[Azure Active Directory] 連結](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

<span data-ttu-id="dc163-257">您現在可以透過 Azure 入口網站為租用戶執行所有 Site Recovery 作業，以及管理災害復原作業。</span><span class="sxs-lookup"><span data-stu-id="dc163-257">You can now perform all site-recovery operations for the tenant through the Azure portal and manage the disaster-recovery operations.</span></span> <span data-ttu-id="dc163-258">若要透過 CSP 存取租用戶訂用帳戶來進行受管理的災害復原，請遵循先前所述的程序。</span><span class="sxs-lookup"><span data-stu-id="dc163-258">To access the tenant subscription through CSP for managed disaster recovery, follow the previously described process.</span></span>

### <a name="step-3-deploy-resources-to-the-tenant-subscription"></a><span data-ttu-id="dc163-259">步驟 3：將資源部署到租用戶訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dc163-259">Step 3: Deploy resources to the tenant subscription</span></span>
1. <span data-ttu-id="dc163-260">在 Azure 入口網站上，建立「資源群組」，然後對於每個一般程序部署「復原服務」保存庫。</span><span class="sxs-lookup"><span data-stu-id="dc163-260">On the Azure portal, create a resource group, and then deploy a Recovery Services vault per the usual process.</span></span> 
 
2. <span data-ttu-id="dc163-261">下載保存庫註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="dc163-261">Download the vault registration key.</span></span>

3. <span data-ttu-id="dc163-262">使用保存庫註冊金鑰為租用戶註冊 CS。</span><span class="sxs-lookup"><span data-stu-id="dc163-262">Register the CS for the tenant by using the vault registration key.</span></span>

4. <span data-ttu-id="dc163-263">輸入兩個存取帳戶 (vCenter 存取帳戶和虛擬機器存取帳戶) 的認證。</span><span class="sxs-lookup"><span data-stu-id="dc163-263">Enter the credentials for the two access accounts: vCenter access account and VM access account.</span></span>

    ![管理員設定伺服器帳戶](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-to-the-recovery-services-vault"></a><span data-ttu-id="dc163-265">步驟 4：向復原服務保存庫註冊 Site Recovery 基礎結構</span><span class="sxs-lookup"><span data-stu-id="dc163-265">Step 4: Register Site Recovery infrastructure to the Recovery Services vault</span></span>
1. <span data-ttu-id="dc163-266">在 Azure 入口網站中，對於稍早建立的保存庫，將 vCenter 伺服器註冊到您在「步驟 3：將資源部署到租用戶訂用帳戶」中註冊的 CS。</span><span class="sxs-lookup"><span data-stu-id="dc163-266">In the Azure portal, on the vault that you created earlier, register the vCenter server to the CS that you registered in "Step 3: Deploy resources to the tenant subscription."</span></span> <span data-ttu-id="dc163-267">將 vCenter 存取帳戶用於此目的。</span><span class="sxs-lookup"><span data-stu-id="dc163-267">Use the vCenter access account for this purpose.</span></span>
2. <span data-ttu-id="dc163-268">針對每個一般程序的 Site Recovery 完成「準備基礎結構」程序。</span><span class="sxs-lookup"><span data-stu-id="dc163-268">Finish the "Prepare infrastructure" process for Site Recovery per the usual process.</span></span>
3. <span data-ttu-id="dc163-269">現在可以開始複寫 VM。</span><span class="sxs-lookup"><span data-stu-id="dc163-269">The VMs are now ready to be replicated.</span></span> <span data-ttu-id="dc163-270">確認 [複寫] 選項下的 [選取虛擬機器] 刀鋒視窗僅顯示租用戶的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dc163-270">Verify that only the tenant’s VMs are displayed on the **Select virtual machines** blade under the **Replicate** option.</span></span>

    ![[選取虛擬機器] 刀鋒視窗上的租用戶虛擬機器清單](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-to-the-subscription"></a><span data-ttu-id="dc163-272">步驟 5︰將對訂用帳戶的存取權指派給租用戶</span><span class="sxs-lookup"><span data-stu-id="dc163-272">Step 5: Assign tenant access to the subscription</span></span>

<span data-ttu-id="dc163-273">對於自助災害復原，向租用戶提供帳戶詳細資料，如「步驟 1：建立租用戶帳戶」一節的步驟 6 所述。</span><span class="sxs-lookup"><span data-stu-id="dc163-273">For self-service disaster recovery, provide to the tenant the account details, as mentioned in step 6 of the "Step 1: Create a tenant account" section.</span></span> <span data-ttu-id="dc163-274">合作夥伴設定災害復原基礎結構之後，請執行此動作。</span><span class="sxs-lookup"><span data-stu-id="dc163-274">Perform this action after the partner sets up the disaster-recovery infrastructure.</span></span> <span data-ttu-id="dc163-275">無論災害復原類型是否為受管理或自助，合作夥伴都必須透過 CSP 入口網站存取租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-275">Whether the disaster-recovery type is managed or self-service, partners must access tenant subscriptions through the CSP portal.</span></span> <span data-ttu-id="dc163-276">合作夥伴可設定合作夥伴擁有的保存庫，並將基礎結構註冊到租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-276">They set up the partner-owned vault and register infrastructure to the tenant subscriptions.</span></span>

<span data-ttu-id="dc163-277">合作夥伴也可以透過 CSP 入口網站將新的使用者加入租用戶訂用帳戶，方法如下：</span><span class="sxs-lookup"><span data-stu-id="dc163-277">Partners can also add a new user to the tenant subscription through the CSP portal by doing the following:</span></span>

1. <span data-ttu-id="dc163-278">移至租用戶的 CSP 訂用帳戶頁面，然後選取 [使用者與授權] 選項。</span><span class="sxs-lookup"><span data-stu-id="dc163-278">Go to the tenant’s CSP subscription page, and then select the **Users and licenses** option.</span></span>

    ![租用戶的 CSP 訂用帳戶頁面](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    <span data-ttu-id="dc163-280">您現在可以輸入相關詳細資料並選取權限，也可以使用 CSV 檔案上傳使用者的清單，以便建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="dc163-280">You can now create a new user by entering the relevant details and selecting permissions or by uploading the list of users in a CSV file.</span></span>

2. <span data-ttu-id="dc163-281">建立新的使用者之後，返回 Azure 入口網站，並在 [訂用帳戶] 刀鋒視窗選取相關訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc163-281">After you've created a new user, go back to the Azure portal, and then, on the **Subscription** blade, select the relevant subscription.</span></span>

3. <span data-ttu-id="dc163-282">在開啟的刀鋒視窗上選取 [存取控制 (IAM)]，然後按一下 [新增] 以使用相關的存取層級新增使用者。</span><span class="sxs-lookup"><span data-stu-id="dc163-282">On the blade that opens, select **Access Control (IAM)**, and then click **Add** to add a user with the relevant access level.</span></span>      
    <span data-ttu-id="dc163-283">在按一下存取層級之後開啟的刀鋒視窗上，會自動顯示透過 CSP 入口網站建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="dc163-283">The users that were created through the CSP portal are automatically displayed on the blade that opens after you click an access level.</span></span>

    ![新增使用者](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    <span data-ttu-id="dc163-285">*參與者*角色就足以執行大多數的管理作業。</span><span class="sxs-lookup"><span data-stu-id="dc163-285">For most management operations, the *Contributor* role is sufficient.</span></span> <span data-ttu-id="dc163-286">除了變更存取層級 (必須具有「擁有者」存取層級) 之外，具有此存取層級的使用者可以在訂用帳戶上執行任何作業。</span><span class="sxs-lookup"><span data-stu-id="dc163-286">Users with this access level can do everything on a subscription except change access levels (for which *Owner*-level access is required).</span></span> <span data-ttu-id="dc163-287">您也可以視需要微調存取層級。</span><span class="sxs-lookup"><span data-stu-id="dc163-287">You can also fine-tune the access levels as required.</span></span>
