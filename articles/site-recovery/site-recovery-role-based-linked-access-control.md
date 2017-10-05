---
title: "使用角色型存取控制來管理 Azure Site Recovery | Microsoft Docs"
description: "本文說明如何套用與使用角色型存取控制 (RBAC) 來管理 Azure Site Recovery 部署"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 9dd74014bf05234a83c7678b67b42b96cd8b8d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-role-based-access-control-to-manage-azure-site-recovery-deployments"></a><span data-ttu-id="35c46-103">使用角色型存取控制管理 Azure Site Recovery 部署</span><span class="sxs-lookup"><span data-stu-id="35c46-103">Use Role-Based Access Control to manage Azure Site Recovery deployments</span></span>

<span data-ttu-id="35c46-104">Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="35c46-104">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="35c46-105">您可以使用 RBAC 劃分小組責任，並只將特定存取權限授與需要執行特定工作的使用者。</span><span class="sxs-lookup"><span data-stu-id="35c46-105">Using RBAC, you can segregate responsibilities within your team and grant only specific access permissions to users as needed to perform specific jobs.</span></span>

<span data-ttu-id="35c46-106">Azure Site Recovery 提供 3 種內建角色，以控制 Site Recovery 管理作業。</span><span class="sxs-lookup"><span data-stu-id="35c46-106">Azure Site Recovery provides 3 built-in roles to control Site Recovery management operations.</span></span> <span data-ttu-id="35c46-107">深入了解 [Azure RBAC 內建角色](../active-directory/role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="35c46-107">Learn more on [Azure RBAC built-in roles](../active-directory/role-based-access-built-in-roles.md)</span></span>

* <span data-ttu-id="35c46-108">[Site Recovery 參與者](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor)：此角色具有在復原服務保存庫中管理 Azure Site Recovery 作業所需的所有權限。</span><span class="sxs-lookup"><span data-stu-id="35c46-108">[Site Recovery Contributor](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) - This role has all permissions required to manage Azure Site Recovery operations in a Recovery Services vault.</span></span> <span data-ttu-id="35c46-109">不過，具有此角色的使用者無法建立或刪除復原服務保存庫，也無法為其他使用者指派存取權限。</span><span class="sxs-lookup"><span data-stu-id="35c46-109">A user with this role, however, can't create or delete a Recovery Services vault or assign access rights to other users.</span></span> <span data-ttu-id="35c46-110">此角色最適合災害復原系統管理員，他們可以為應用程式或整個組織 (視情況而定) 啟用和管理災害復原。</span><span class="sxs-lookup"><span data-stu-id="35c46-110">This role is best suited for disaster recovery administrators who can enable and manage disaster recovery for applications or entire organizations, as the case may be.</span></span>
* <span data-ttu-id="35c46-111">[Site Recovery 操作員](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator)：此角色具有執行和管理容錯移轉和容錯回復作業的權限。</span><span class="sxs-lookup"><span data-stu-id="35c46-111">[Site Recovery Operator](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) - This role has permissions to execute and manager Failover and Failback operations.</span></span> <span data-ttu-id="35c46-112">具有此角色的使用者無法啟用或停用複寫、建立或刪除保存庫、註冊新的基礎結構，也無法為其他使用者指派存取權限。</span><span class="sxs-lookup"><span data-stu-id="35c46-112">A user with this role can't enable or disable replication, create or delete vaults, register new infrastructure or assign access rights to other users.</span></span> <span data-ttu-id="35c46-113">此角色最適合災害復原操作員，當應用程式擁有者和 IT 系統管理員在實際或模擬災害情況 (例如災害復原演習) 中指示時，操作員可以對虛擬機器或應用程式進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="35c46-113">This role is best suited for a disaster recovery operator who can failover virtual machines or applications when instructed by application owners and IT administrators in an actual or simulated disaster situation such as a DR drill.</span></span> <span data-ttu-id="35c46-114">災害解決後，災害復原操作員可以重新保護和容錯回復虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="35c46-114">Post resolution of the disaster, the DR operator can re-protect and failback the virtual machines.</span></span>
* <span data-ttu-id="35c46-115">[Site Recovery 讀者](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader)：此角色擁有可檢視所有 Site Recovery 管理作業的權限。</span><span class="sxs-lookup"><span data-stu-id="35c46-115">[Site Recovery Reader](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) - This role has permissions to view all Site Recovery management operations.</span></span> <span data-ttu-id="35c46-116">此角色最適合 IT 監督主管，以便監控目前的保護狀態，並在需要時提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="35c46-116">This role is best suited for an IT monitoring executive who can monitor the current state of protection and raise support tickets if required.</span></span>

<span data-ttu-id="35c46-117">如果您想要定義自己的角色以獲得更進一步控制，請參閱如何在 Azure 中[建立自訂角色](../active-directory/role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="35c46-117">If you're looking to define your own roles for even more control, see how to [build Custom roles](../active-directory/role-based-access-control-custom-roles.md) in Azure.</span></span>

## <a name="permissions-required-to-enable-replication-for-new-virtual-machines"></a><span data-ttu-id="35c46-118">啟用新虛擬機器複寫所需的權限</span><span class="sxs-lookup"><span data-stu-id="35c46-118">Permissions required to Enable Replication for new Virtual Machines</span></span>
<span data-ttu-id="35c46-119">當使用 Azure Site Recovery 將新的虛擬機器複寫至 Azure 時，系統會驗證相關聯使用者的存取層級，以確定使用者擁有使用提供給 Site Recovery 的 Azure 資源所需的權限。</span><span class="sxs-lookup"><span data-stu-id="35c46-119">When a new Virtual Machine is replicated to Azure using Azure Site Recovery, the associated user's access levels are validated to ensure that the user has the required permissions to use the Azure resources provided to Site Recovery.</span></span>

<span data-ttu-id="35c46-120">若要啟用新虛擬機器的複寫，使用者必須擁有：</span><span class="sxs-lookup"><span data-stu-id="35c46-120">To enable replication for a new virtual machine, a user must have:</span></span>
* <span data-ttu-id="35c46-121">在所選資源群組中建立虛擬機器的權限</span><span class="sxs-lookup"><span data-stu-id="35c46-121">Permission to create a virtual machine in the selected resource group</span></span>
* <span data-ttu-id="35c46-122">在所選虛擬網路中建立虛擬機器的權限</span><span class="sxs-lookup"><span data-stu-id="35c46-122">Permission to create a virtual machine in the selected virtual network</span></span>
* <span data-ttu-id="35c46-123">寫入所選儲存體帳戶的權限</span><span class="sxs-lookup"><span data-stu-id="35c46-123">Permission to write to the selected Storage account</span></span>

<span data-ttu-id="35c46-124">使用者需要下列權限才能完成新虛擬機器的複寫。</span><span class="sxs-lookup"><span data-stu-id="35c46-124">A user needs the following permissions to complete replication of a new virtual machine.</span></span>

> [!IMPORTANT]
><span data-ttu-id="35c46-125">確定為每個用於部署資源的部署模型 (Resource Manager/傳統) 新增相關的權限。</span><span class="sxs-lookup"><span data-stu-id="35c46-125">Ensure that relevant permissions are added per the deployment model (Resource Manager/ Classic) used for resource deployment.</span></span>

| <span data-ttu-id="35c46-126">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="35c46-126">**Resource Type**</span></span> | <span data-ttu-id="35c46-127">**部署模型**</span><span class="sxs-lookup"><span data-stu-id="35c46-127">**Deployment Model**</span></span> | <span data-ttu-id="35c46-128">**權限**</span><span class="sxs-lookup"><span data-stu-id="35c46-128">**Permission**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35c46-129">計算</span><span class="sxs-lookup"><span data-stu-id="35c46-129">Compute</span></span> | <span data-ttu-id="35c46-130">資源管理員</span><span class="sxs-lookup"><span data-stu-id="35c46-130">Resource Manager</span></span> | <span data-ttu-id="35c46-131">Microsoft.Compute/availabilitySets/read</span><span class="sxs-lookup"><span data-stu-id="35c46-131">Microsoft.Compute/availabilitySets/read</span></span> |
|  |  | <span data-ttu-id="35c46-132">Microsoft.Compute/virtualMachines/read</span><span class="sxs-lookup"><span data-stu-id="35c46-132">Microsoft.Compute/virtualMachines/read</span></span> |
|  |  | <span data-ttu-id="35c46-133">Microsoft.Compute/virtualMachines/write</span><span class="sxs-lookup"><span data-stu-id="35c46-133">Microsoft.Compute/virtualMachines/write</span></span> |
|  |  | <span data-ttu-id="35c46-134">Microsoft.Compute/virtualMachines/delete</span><span class="sxs-lookup"><span data-stu-id="35c46-134">Microsoft.Compute/virtualMachines/delete</span></span> |
|  | <span data-ttu-id="35c46-135">傳統</span><span class="sxs-lookup"><span data-stu-id="35c46-135">Classic</span></span> | <span data-ttu-id="35c46-136">Microsoft.ClassicCompute/domainNames/read</span><span class="sxs-lookup"><span data-stu-id="35c46-136">Microsoft.ClassicCompute/domainNames/read</span></span> |
|  |  | <span data-ttu-id="35c46-137">Microsoft.ClassicCompute/domainNames/write</span><span class="sxs-lookup"><span data-stu-id="35c46-137">Microsoft.ClassicCompute/domainNames/write</span></span> |
|  |  | <span data-ttu-id="35c46-138">Microsoft.ClassicCompute/domainNames/delete</span><span class="sxs-lookup"><span data-stu-id="35c46-138">Microsoft.ClassicCompute/domainNames/delete</span></span> |
|  |  | <span data-ttu-id="35c46-139">Microsoft.ClassicCompute/virtualMachines/read</span><span class="sxs-lookup"><span data-stu-id="35c46-139">Microsoft.ClassicCompute/virtualMachines/read</span></span> |
|  |  | <span data-ttu-id="35c46-140">Microsoft.ClassicCompute/virtualMachines/write</span><span class="sxs-lookup"><span data-stu-id="35c46-140">Microsoft.ClassicCompute/virtualMachines/write</span></span> |
|  |  | <span data-ttu-id="35c46-141">Microsoft.ClassicCompute/virtualMachines/delete</span><span class="sxs-lookup"><span data-stu-id="35c46-141">Microsoft.ClassicCompute/virtualMachines/delete</span></span> |
| <span data-ttu-id="35c46-142">網路</span><span class="sxs-lookup"><span data-stu-id="35c46-142">Network</span></span> | <span data-ttu-id="35c46-143">資源管理員</span><span class="sxs-lookup"><span data-stu-id="35c46-143">Resource Manager</span></span> | <span data-ttu-id="35c46-144">Microsoft.Network/networkInterfaces/read</span><span class="sxs-lookup"><span data-stu-id="35c46-144">Microsoft.Network/networkInterfaces/read</span></span> |
|  |  | <span data-ttu-id="35c46-145">Microsoft.Network/networkInterfaces/write</span><span class="sxs-lookup"><span data-stu-id="35c46-145">Microsoft.Network/networkInterfaces/write</span></span> |
|  |  | <span data-ttu-id="35c46-146">Microsoft.Network/networkInterfaces/delete</span><span class="sxs-lookup"><span data-stu-id="35c46-146">Microsoft.Network/networkInterfaces/delete</span></span> |
|  |  | <span data-ttu-id="35c46-147">Microsoft.Network/networkInterfaces/join/action</span><span class="sxs-lookup"><span data-stu-id="35c46-147">Microsoft.Network/networkInterfaces/join/action</span></span> |
|  |  | <span data-ttu-id="35c46-148">Microsoft.Network/virtualNetworks/read</span><span class="sxs-lookup"><span data-stu-id="35c46-148">Microsoft.Network/virtualNetworks/read</span></span> |
|  |  | <span data-ttu-id="35c46-149">Microsoft.Network/virtualNetworks/subnets/read</span><span class="sxs-lookup"><span data-stu-id="35c46-149">Microsoft.Network/virtualNetworks/subnets/read</span></span> |
|  |  | <span data-ttu-id="35c46-150">Microsoft.Network/virtualNetworks/subnets/join/action</span><span class="sxs-lookup"><span data-stu-id="35c46-150">Microsoft.Network/virtualNetworks/subnets/join/action</span></span> |
|  | <span data-ttu-id="35c46-151">傳統</span><span class="sxs-lookup"><span data-stu-id="35c46-151">Classic</span></span> | <span data-ttu-id="35c46-152">Microsoft.ClassicNetwork/virtualNetworks/read</span><span class="sxs-lookup"><span data-stu-id="35c46-152">Microsoft.ClassicNetwork/virtualNetworks/read</span></span> |
|  |  | <span data-ttu-id="35c46-153">Microsoft.ClassicNetwork/virtualNetworks/join/action</span><span class="sxs-lookup"><span data-stu-id="35c46-153">Microsoft.ClassicNetwork/virtualNetworks/join/action</span></span> |
| <span data-ttu-id="35c46-154">儲存體</span><span class="sxs-lookup"><span data-stu-id="35c46-154">Storage</span></span> | <span data-ttu-id="35c46-155">資源管理員</span><span class="sxs-lookup"><span data-stu-id="35c46-155">Resource Manager</span></span> | <span data-ttu-id="35c46-156">Microsoft.Storage/storageAccounts/read</span><span class="sxs-lookup"><span data-stu-id="35c46-156">Microsoft.Storage/storageAccounts/read</span></span> |
|  |  | <span data-ttu-id="35c46-157">Microsoft.Storage/storageAccounts/listkeys/action</span><span class="sxs-lookup"><span data-stu-id="35c46-157">Microsoft.Storage/storageAccounts/listkeys/action</span></span> |
|  | <span data-ttu-id="35c46-158">傳統</span><span class="sxs-lookup"><span data-stu-id="35c46-158">Classic</span></span> | <span data-ttu-id="35c46-159">Microsoft.ClassicStorage/storageAccounts/read</span><span class="sxs-lookup"><span data-stu-id="35c46-159">Microsoft.ClassicStorage/storageAccounts/read</span></span> |
|  |  | <span data-ttu-id="35c46-160">Microsoft.ClassicStorage/storageAccounts/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="35c46-160">Microsoft.ClassicStorage/storageAccounts/listKeys/action</span></span> |
| <span data-ttu-id="35c46-161">資源群組</span><span class="sxs-lookup"><span data-stu-id="35c46-161">Resource Group</span></span> | <span data-ttu-id="35c46-162">資源管理員</span><span class="sxs-lookup"><span data-stu-id="35c46-162">Resource Manager</span></span> | <span data-ttu-id="35c46-163">Microsoft.Resources/deployments/*</span><span class="sxs-lookup"><span data-stu-id="35c46-163">Microsoft.Resources/deployments/*</span></span> |
|  |  | <span data-ttu-id="35c46-164">Microsoft.Resources/subscriptions/resourceGroups/read</span><span class="sxs-lookup"><span data-stu-id="35c46-164">Microsoft.Resources/subscriptions/resourceGroups/read</span></span> |

<span data-ttu-id="35c46-165">請考慮分別為 Resource Manager 與傳統部署模型使用「虛擬機器參與者」與「傳統虛擬機器參與者」[內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="35c46-165">Consider using the 'Virtual Machine Contributor' and 'Classic Virtual Machine Contributor' [built-in roles](../active-directory/role-based-access-built-in-roles.md) for Resource Manager and Classic deployment models respectively.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35c46-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35c46-166">Next steps</span></span>
* <span data-ttu-id="35c46-167">[角色型存取控制](../active-directory/role-based-access-control-configure.md)：開始在 Azure 入口網站中使用 RBAC。</span><span class="sxs-lookup"><span data-stu-id="35c46-167">[Role-Based Access Control](../active-directory/role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="35c46-168">了解如何使用下列各項管理存取權：</span><span class="sxs-lookup"><span data-stu-id="35c46-168">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="35c46-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35c46-169">PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="35c46-170">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="35c46-170">Azure CLI</span></span>](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="35c46-171">REST API</span><span class="sxs-lookup"><span data-stu-id="35c46-171">REST API</span></span>](../active-directory/role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="35c46-172">[角色型存取控制疑難排解](../active-directory/role-based-access-control-troubleshooting.md)︰取得修正常見問題的建議。</span><span class="sxs-lookup"><span data-stu-id="35c46-172">[Role-Based Access Control troubleshooting](../active-directory/role-based-access-control-troubleshooting.md): Get suggestions for fixing common issues.</span></span>
