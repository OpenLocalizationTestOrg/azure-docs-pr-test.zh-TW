---
title: "刪除 Site Recovery 保存庫"
description: "瞭解如何根據 Site Recovery 案例刪除 Azure Site Recovery 保存庫。"
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
ms.openlocfilehash: b95b9defa0a037f7d7d3ef36b99bc7c53c751050
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="432a7-103">刪除 Site Recovery 保存庫</span><span class="sxs-lookup"><span data-stu-id="432a7-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="432a7-104">相依性會阻擋您刪除 Azure Site Recovery 保存庫。</span><span class="sxs-lookup"><span data-stu-id="432a7-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="432a7-105">您需要採取的動作隨 Site Recovery 案例而異：VMware 到 Azure、HYPER-V (附與不附 System Center Virtual Machine Manager) 到 Azure，以及 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="432a7-105">The actions you need to take vary based on the Site Recovery scenario: VMware to Azure, Hyper-V (with and without System Center Virtual Machine Manager) to Azure, and Azure Backup.</span></span> <span data-ttu-id="432a7-106">若要刪除 Azure 備份使用的保存庫，請參閱[刪除 Azure 中的備份保存庫](../backup/backup-azure-delete-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="432a7-106">To delete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="432a7-107">如果您要測試產品，且不在乎資料遺失問題，可使用強制刪除方法快速移除保存庫及其所有相依性。</span><span class="sxs-lookup"><span data-stu-id="432a7-107">If you're testing the product and aren't concerned about data loss, use the force delete method to rapidly remove the vault and all its dependencies.</span></span>

> <span data-ttu-id="432a7-108">PowerShell 命令會刪除保存庫的所有內容，而且此步驟無法復原。</span><span class="sxs-lookup"><span data-stu-id="432a7-108">The PowerShell command deletes all the contents of the vault and is not reversible.</span></span>

## <a name="use-powershell-to-force-delete-the-vault"></a><span data-ttu-id="432a7-109">使用 PowerShell 強制刪除保存庫</span><span class="sxs-lookup"><span data-stu-id="432a7-109">Use PowerShell to force delete the vault</span></span> 

<span data-ttu-id="432a7-110">即使有受保護的項目也要刪除 Site Recovery 保存庫，請使用這些命令：</span><span class="sxs-lookup"><span data-stu-id="432a7-110">To delete the Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="432a7-111">刪除 Site Recovery 保存庫</span><span class="sxs-lookup"><span data-stu-id="432a7-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="432a7-112">請依照針對您案例的建議步驟刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="432a7-112">To delete the vault, follow the recommended steps for your scenario.</span></span>

### <a name="vmware-vms-to-azure"></a><span data-ttu-id="432a7-113">VMware VM 至 Azure</span><span class="sxs-lookup"><span data-stu-id="432a7-113">VMware VMs to Azure</span></span>

1. <span data-ttu-id="432a7-114">依照[停用 VMware 保護](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)中的步驟刪除所有受保護的 VM。</span><span class="sxs-lookup"><span data-stu-id="432a7-114">Delete all protected VMs by following the steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="432a7-115">依照[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。中的步驟刪除所有複寫原則。</span><span class="sxs-lookup"><span data-stu-id="432a7-115">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="432a7-116">依照[刪除 vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery) 中的步驟刪除 vCenter 的參考。</span><span class="sxs-lookup"><span data-stu-id="432a7-116">Delete references to vCenter by following the steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="432a7-117">依照[解除委任的組態伺服器](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server)中的步驟刪除組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="432a7-117">Delete the configuration server by following the steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="432a7-118">刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="432a7-118">Delete the vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-to-azure"></a><span data-ttu-id="432a7-119">Hyper-V VM (附 Virtual Machine Manager) 到 Azure</span><span class="sxs-lookup"><span data-stu-id="432a7-119">Hyper-V VMs (with Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="432a7-120">依照[停用 VMware VM 或實體伺服器的保護](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)中的步驟刪除所有受保護的 VM。</span><span class="sxs-lookup"><span data-stu-id="432a7-120">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="432a7-121">依照[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。中的步驟刪除所有複寫原則。</span><span class="sxs-lookup"><span data-stu-id="432a7-121">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="432a7-122">依照[取消登錄已連線的 VMM 伺服器](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server)中的步驟刪除 Virtual Machine Manager 伺服器的參考。</span><span class="sxs-lookup"><span data-stu-id="432a7-122">Delete references to Virtual Machine Manager servers by following the steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="432a7-123">刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="432a7-123">Delete the vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-to-azure"></a><span data-ttu-id="432a7-124">Hyper-V VM (不附 Virtual Machine Manager) 到 Azure</span><span class="sxs-lookup"><span data-stu-id="432a7-124">Hyper-V VMs (without Virtual Machine Manager) to Azure</span></span>
1. <span data-ttu-id="432a7-125">依照[停用 VMware VM 或實體伺服器的保護](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)中的步驟刪除所有受保護的 VM。</span><span class="sxs-lookup"><span data-stu-id="432a7-125">Delete all protected VMs by following the steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="432a7-126">依照[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。中的步驟刪除所有複寫原則。</span><span class="sxs-lookup"><span data-stu-id="432a7-126">Delete all replication policies by following the steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="432a7-127">依照[取消登錄 HYPER-V 主機](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site)中的步驟來刪除 HYPER-V 伺服器的參考。</span><span class="sxs-lookup"><span data-stu-id="432a7-127">Delete references to Hyper-V servers by following the steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="432a7-128">刪除 Hyper-V 站台。</span><span class="sxs-lookup"><span data-stu-id="432a7-128">Delete the Hyper-V site.</span></span>

5. <span data-ttu-id="432a7-129">刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="432a7-129">Delete the vault.</span></span>
