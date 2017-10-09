---
title: "aaaDelete Site Recovery 保存庫"
description: "了解如何 toodelete Azure Site Recovery 保存庫中，根據 hello 站台復原案例。"
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="61e2f-103">刪除 Site Recovery 保存庫</span><span class="sxs-lookup"><span data-stu-id="61e2f-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="61e2f-104">相依性會阻擋您刪除 Azure Site Recovery 保存庫。</span><span class="sxs-lookup"><span data-stu-id="61e2f-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="61e2f-105">hello 需要 tootake 動作而異 hello 站台復原案例： VMware tooAzure HYPER-V （含與不含 「 System Center Virtual Machine Manager） tooAzure 和 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="61e2f-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="61e2f-106">請參閱 toodelete 用於 Azure 備份保存庫[刪除備份保存庫在 Azure 中的](../backup/backup-azure-delete-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="61e2f-107">如果您正在測試 hello 產品，不必擔心資料遺失時，使用 hello 強制刪除方法 toorapidly 移除 hello 保存庫和其所有相依性。</span><span class="sxs-lookup"><span data-stu-id="61e2f-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="61e2f-108">hello PowerShell 命令會刪除所有 hello 內容 hello 保存庫和之後即無法復原。</span><span class="sxs-lookup"><span data-stu-id="61e2f-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="61e2f-109">使用 PowerShell tooforce 刪除 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="61e2f-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="61e2f-110">站台復原保存庫，即使有 toodelete hello 受保護的項目，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="61e2f-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="61e2f-111">刪除 Site Recovery 保存庫</span><span class="sxs-lookup"><span data-stu-id="61e2f-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="61e2f-112">toodelete hello 保存庫，後續 hello 建議用於您案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="61e2f-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="61e2f-113">VMware Vm tooAzure</span><span class="sxs-lookup"><span data-stu-id="61e2f-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="61e2f-114">中的 hello 步驟來刪除所有受保護的 Vm[停用保護，適用於 VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="61e2f-115">刪除所有的複寫原則中的 hello 步驟[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="61e2f-116">刪除的參考中的步驟的下列 hello toovCenter[刪除 vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="61e2f-117">刪除 hello 組態伺服器中的 hello 步驟[解除委任的組態伺服器](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="61e2f-118">刪除 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="61e2f-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="61e2f-119">HYPER-V Vm (與 Virtual Machine Manager) tooAzure</span><span class="sxs-lookup"><span data-stu-id="61e2f-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="61e2f-120">中的 hello 步驟來刪除所有受保護的 Vm[停用保護 VMware VM 或實體伺服器](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="61e2f-121">刪除所有的複寫原則中的 hello 步驟[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="61e2f-122">刪除參考 tooVirtual Machine Manager 伺服器中的 hello 步驟[已連線的 VMM 伺服器取消登錄](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="61e2f-123">刪除 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="61e2f-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="61e2f-124">(不含 Virtual Machine Manager) 的 HYPER-V Vm tooAzure</span><span class="sxs-lookup"><span data-stu-id="61e2f-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="61e2f-125">中的 hello 步驟來刪除所有受保護的 Vm[停用保護 VMware VM 或實體伺服器](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="61e2f-126">刪除所有的複寫原則中的 hello 步驟[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="61e2f-127">刪除參考 tooHyper APP-V 伺服器中的 hello 步驟[取消註冊 HYPER-V 主機](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site)。</span><span class="sxs-lookup"><span data-stu-id="61e2f-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="61e2f-128">刪除 hello HYPER-V 站台。</span><span class="sxs-lookup"><span data-stu-id="61e2f-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="61e2f-129">刪除 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="61e2f-129">Delete hello vault.</span></span>
