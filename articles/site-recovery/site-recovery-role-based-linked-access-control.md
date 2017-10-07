---
title: "aaaUsing 角色型存取控制 toomanage Azure Site Recovery |Microsoft 文件"
description: "本文說明如何 tooapply 和使用角色型存取控制 (RBAC) toomanage Azure Site Recovery 部署"
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
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a><span data-ttu-id="b8a67-103">使用角色型存取控制 toomanage Azure Site Recovery 部署</span><span class="sxs-lookup"><span data-stu-id="b8a67-103">Use Role-Based Access Control toomanage Azure Site Recovery deployments</span></span>

<span data-ttu-id="b8a67-104">Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="b8a67-104">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="b8a67-105">使用 RBAC 時，您可以隔離您的小組內的責任，並授與僅特定存取權限 toousers 需要的 tooperform 特定工作的形式。</span><span class="sxs-lookup"><span data-stu-id="b8a67-105">Using RBAC, you can segregate responsibilities within your team and grant only specific access permissions toousers as needed tooperform specific jobs.</span></span>

<span data-ttu-id="b8a67-106">Azure Site Recovery 提供 3 的內建角色 toocontrol Site Recovery 管理作業。</span><span class="sxs-lookup"><span data-stu-id="b8a67-106">Azure Site Recovery provides 3 built-in roles toocontrol Site Recovery management operations.</span></span> <span data-ttu-id="b8a67-107">深入了解 [Azure RBAC 內建角色](../active-directory/role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="b8a67-107">Learn more on [Azure RBAC built-in roles](../active-directory/role-based-access-built-in-roles.md)</span></span>

* <span data-ttu-id="b8a67-108">[站台復原參與者](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor)-這個角色具有所有使用權限必要的 toomanage Azure Site Recovery 作業復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="b8a67-108">[Site Recovery Contributor](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) - This role has all permissions required toomanage Azure Site Recovery operations in a Recovery Services vault.</span></span> <span data-ttu-id="b8a67-109">使用者與此角色，不過，無法建立或刪除復原服務保存庫或指派存取權限 tooother 使用者。</span><span class="sxs-lookup"><span data-stu-id="b8a67-109">A user with this role, however, can't create or delete a Recovery Services vault or assign access rights tooother users.</span></span> <span data-ttu-id="b8a67-110">此角色最適合用於災害復原的系統管理員可以啟用和管理的應用程式或整個組織，嚴重損壞修復作為可能 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="b8a67-110">This role is best suited for disaster recovery administrators who can enable and manage disaster recovery for applications or entire organizations, as hello case may be.</span></span>
* <span data-ttu-id="b8a67-111">[站台復原操作員](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator)-這個角色有權限 tooexecute 和管理員容錯移轉和容錯回復作業。</span><span class="sxs-lookup"><span data-stu-id="b8a67-111">[Site Recovery Operator](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) - This role has permissions tooexecute and manager Failover and Failback operations.</span></span> <span data-ttu-id="b8a67-112">具有此角色的使用者無法啟用或停用複寫，建立或刪除保存庫，註冊新的基礎結構或指派存取權限 tooother 使用者。</span><span class="sxs-lookup"><span data-stu-id="b8a67-112">A user with this role can't enable or disable replication, create or delete vaults, register new infrastructure or assign access rights tooother users.</span></span> <span data-ttu-id="b8a67-113">此角色最適合災害復原操作員，當應用程式擁有者和 IT 系統管理員在實際或模擬災害情況 (例如災害復原演習) 中指示時，操作員可以對虛擬機器或應用程式進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b8a67-113">This role is best suited for a disaster recovery operator who can failover virtual machines or applications when instructed by application owners and IT administrators in an actual or simulated disaster situation such as a DR drill.</span></span> <span data-ttu-id="b8a67-114">Post hello 災害的解析度，hello DR 運算子可以重新保護和容錯回復 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8a67-114">Post resolution of hello disaster, hello DR operator can re-protect and failback hello virtual machines.</span></span>
* <span data-ttu-id="b8a67-115">[站台復原的讀取器](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader)-這個角色有權限 tooview 站台復原的所有管理作業。</span><span class="sxs-lookup"><span data-stu-id="b8a67-115">[Site Recovery Reader](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) - This role has permissions tooview all Site Recovery management operations.</span></span> <span data-ttu-id="b8a67-116">這個角色是保護的適用於 IT 監視主管人員可以監視 hello 的目前狀態，並引發支援票證，必要的。</span><span class="sxs-lookup"><span data-stu-id="b8a67-116">This role is best suited for an IT monitoring executive who can monitor hello current state of protection and raise support tickets if required.</span></span>

<span data-ttu-id="b8a67-117">如果您要尋找 toodefine 您自己的角色的更多控制，請參閱如何太[建置自訂角色](../active-directory/role-based-access-control-custom-roles.md)在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="b8a67-117">If you're looking toodefine your own roles for even more control, see how too[build Custom roles](../active-directory/role-based-access-control-custom-roles.md) in Azure.</span></span>

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a><span data-ttu-id="b8a67-118">TooEnable 複寫所需的新虛擬機器權限</span><span class="sxs-lookup"><span data-stu-id="b8a67-118">Permissions required tooEnable Replication for new Virtual Machines</span></span>
<span data-ttu-id="b8a67-119">使用 Azure Site Recovery 的複寫的 tooAzure 新的虛擬機器時，相關聯的 hello 使用者的存取層級是 hello 使用者的驗證的 tooensure hello 具有必要權限 toouse hello Azure 提供的資源 tooSite 復原。</span><span class="sxs-lookup"><span data-stu-id="b8a67-119">When a new Virtual Machine is replicated tooAzure using Azure Site Recovery, hello associated user's access levels are validated tooensure that hello user has hello required permissions toouse hello Azure resources provided tooSite Recovery.</span></span>

<span data-ttu-id="b8a67-120">新的虛擬機器的 tooenable 複寫，使用者必須具備：</span><span class="sxs-lookup"><span data-stu-id="b8a67-120">tooenable replication for a new virtual machine, a user must have:</span></span>
* <span data-ttu-id="b8a67-121">權限 toocreate hello 選取的資源群組中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b8a67-121">Permission toocreate a virtual machine in hello selected resource group</span></span>
* <span data-ttu-id="b8a67-122">權限 toocreate hello 選取的虛擬網路中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b8a67-122">Permission toocreate a virtual machine in hello selected virtual network</span></span>
* <span data-ttu-id="b8a67-123">權限 toowrite toohello 選取儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b8a67-123">Permission toowrite toohello selected Storage account</span></span>

<span data-ttu-id="b8a67-124">使用者需要下列權限 toocomplete 複寫新的虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8a67-124">A user needs hello following permissions toocomplete replication of a new virtual machine.</span></span>

> [!IMPORTANT]
><span data-ttu-id="b8a67-125">請確認相關的權限會新增每個 hello 部署模型 (資源管理員 / 傳統) 資源部署所用的。</span><span class="sxs-lookup"><span data-stu-id="b8a67-125">Ensure that relevant permissions are added per hello deployment model (Resource Manager/ Classic) used for resource deployment.</span></span>

| <span data-ttu-id="b8a67-126">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="b8a67-126">**Resource Type**</span></span> | <span data-ttu-id="b8a67-127">**部署模型**</span><span class="sxs-lookup"><span data-stu-id="b8a67-127">**Deployment Model**</span></span> | <span data-ttu-id="b8a67-128">**權限**</span><span class="sxs-lookup"><span data-stu-id="b8a67-128">**Permission**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8a67-129">計算</span><span class="sxs-lookup"><span data-stu-id="b8a67-129">Compute</span></span> | <span data-ttu-id="b8a67-130">資源管理員</span><span class="sxs-lookup"><span data-stu-id="b8a67-130">Resource Manager</span></span> | <span data-ttu-id="b8a67-131">Microsoft.Compute/availabilitySets/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-131">Microsoft.Compute/availabilitySets/read</span></span> |
|  |  | <span data-ttu-id="b8a67-132">Microsoft.Compute/virtualMachines/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-132">Microsoft.Compute/virtualMachines/read</span></span> |
|  |  | <span data-ttu-id="b8a67-133">Microsoft.Compute/virtualMachines/write</span><span class="sxs-lookup"><span data-stu-id="b8a67-133">Microsoft.Compute/virtualMachines/write</span></span> |
|  |  | <span data-ttu-id="b8a67-134">Microsoft.Compute/virtualMachines/delete</span><span class="sxs-lookup"><span data-stu-id="b8a67-134">Microsoft.Compute/virtualMachines/delete</span></span> |
|  | <span data-ttu-id="b8a67-135">傳統</span><span class="sxs-lookup"><span data-stu-id="b8a67-135">Classic</span></span> | <span data-ttu-id="b8a67-136">Microsoft.ClassicCompute/domainNames/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-136">Microsoft.ClassicCompute/domainNames/read</span></span> |
|  |  | <span data-ttu-id="b8a67-137">Microsoft.ClassicCompute/domainNames/write</span><span class="sxs-lookup"><span data-stu-id="b8a67-137">Microsoft.ClassicCompute/domainNames/write</span></span> |
|  |  | <span data-ttu-id="b8a67-138">Microsoft.ClassicCompute/domainNames/delete</span><span class="sxs-lookup"><span data-stu-id="b8a67-138">Microsoft.ClassicCompute/domainNames/delete</span></span> |
|  |  | <span data-ttu-id="b8a67-139">Microsoft.ClassicCompute/virtualMachines/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-139">Microsoft.ClassicCompute/virtualMachines/read</span></span> |
|  |  | <span data-ttu-id="b8a67-140">Microsoft.ClassicCompute/virtualMachines/write</span><span class="sxs-lookup"><span data-stu-id="b8a67-140">Microsoft.ClassicCompute/virtualMachines/write</span></span> |
|  |  | <span data-ttu-id="b8a67-141">Microsoft.ClassicCompute/virtualMachines/delete</span><span class="sxs-lookup"><span data-stu-id="b8a67-141">Microsoft.ClassicCompute/virtualMachines/delete</span></span> |
| <span data-ttu-id="b8a67-142">網路</span><span class="sxs-lookup"><span data-stu-id="b8a67-142">Network</span></span> | <span data-ttu-id="b8a67-143">資源管理員</span><span class="sxs-lookup"><span data-stu-id="b8a67-143">Resource Manager</span></span> | <span data-ttu-id="b8a67-144">Microsoft.Network/networkInterfaces/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-144">Microsoft.Network/networkInterfaces/read</span></span> |
|  |  | <span data-ttu-id="b8a67-145">Microsoft.Network/networkInterfaces/write</span><span class="sxs-lookup"><span data-stu-id="b8a67-145">Microsoft.Network/networkInterfaces/write</span></span> |
|  |  | <span data-ttu-id="b8a67-146">Microsoft.Network/networkInterfaces/delete</span><span class="sxs-lookup"><span data-stu-id="b8a67-146">Microsoft.Network/networkInterfaces/delete</span></span> |
|  |  | <span data-ttu-id="b8a67-147">Microsoft.Network/networkInterfaces/join/action</span><span class="sxs-lookup"><span data-stu-id="b8a67-147">Microsoft.Network/networkInterfaces/join/action</span></span> |
|  |  | <span data-ttu-id="b8a67-148">Microsoft.Network/virtualNetworks/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-148">Microsoft.Network/virtualNetworks/read</span></span> |
|  |  | <span data-ttu-id="b8a67-149">Microsoft.Network/virtualNetworks/subnets/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-149">Microsoft.Network/virtualNetworks/subnets/read</span></span> |
|  |  | <span data-ttu-id="b8a67-150">Microsoft.Network/virtualNetworks/subnets/join/action</span><span class="sxs-lookup"><span data-stu-id="b8a67-150">Microsoft.Network/virtualNetworks/subnets/join/action</span></span> |
|  | <span data-ttu-id="b8a67-151">傳統</span><span class="sxs-lookup"><span data-stu-id="b8a67-151">Classic</span></span> | <span data-ttu-id="b8a67-152">Microsoft.ClassicNetwork/virtualNetworks/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-152">Microsoft.ClassicNetwork/virtualNetworks/read</span></span> |
|  |  | <span data-ttu-id="b8a67-153">Microsoft.ClassicNetwork/virtualNetworks/join/action</span><span class="sxs-lookup"><span data-stu-id="b8a67-153">Microsoft.ClassicNetwork/virtualNetworks/join/action</span></span> |
| <span data-ttu-id="b8a67-154">儲存體</span><span class="sxs-lookup"><span data-stu-id="b8a67-154">Storage</span></span> | <span data-ttu-id="b8a67-155">資源管理員</span><span class="sxs-lookup"><span data-stu-id="b8a67-155">Resource Manager</span></span> | <span data-ttu-id="b8a67-156">Microsoft.Storage/storageAccounts/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-156">Microsoft.Storage/storageAccounts/read</span></span> |
|  |  | <span data-ttu-id="b8a67-157">Microsoft.Storage/storageAccounts/listkeys/action</span><span class="sxs-lookup"><span data-stu-id="b8a67-157">Microsoft.Storage/storageAccounts/listkeys/action</span></span> |
|  | <span data-ttu-id="b8a67-158">傳統</span><span class="sxs-lookup"><span data-stu-id="b8a67-158">Classic</span></span> | <span data-ttu-id="b8a67-159">Microsoft.ClassicStorage/storageAccounts/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-159">Microsoft.ClassicStorage/storageAccounts/read</span></span> |
|  |  | <span data-ttu-id="b8a67-160">Microsoft.ClassicStorage/storageAccounts/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="b8a67-160">Microsoft.ClassicStorage/storageAccounts/listKeys/action</span></span> |
| <span data-ttu-id="b8a67-161">資源群組</span><span class="sxs-lookup"><span data-stu-id="b8a67-161">Resource Group</span></span> | <span data-ttu-id="b8a67-162">資源管理員</span><span class="sxs-lookup"><span data-stu-id="b8a67-162">Resource Manager</span></span> | <span data-ttu-id="b8a67-163">Microsoft.Resources/deployments/*</span><span class="sxs-lookup"><span data-stu-id="b8a67-163">Microsoft.Resources/deployments/*</span></span> |
|  |  | <span data-ttu-id="b8a67-164">Microsoft.Resources/subscriptions/resourceGroups/read</span><span class="sxs-lookup"><span data-stu-id="b8a67-164">Microsoft.Resources/subscriptions/resourceGroups/read</span></span> |

<span data-ttu-id="b8a67-165">請考慮使用 hello '虛擬機器參與者' 和 '傳統虛擬機器參與者'[內建角色](../active-directory/role-based-access-built-in-roles.md)資源管理員] 和 [傳統部署模型分別。</span><span class="sxs-lookup"><span data-stu-id="b8a67-165">Consider using hello 'Virtual Machine Contributor' and 'Classic Virtual Machine Contributor' [built-in roles](../active-directory/role-based-access-built-in-roles.md) for Resource Manager and Classic deployment models respectively.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8a67-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8a67-166">Next steps</span></span>
* <span data-ttu-id="b8a67-167">[角色型存取控制](../active-directory/role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b8a67-167">[Role-Based Access Control](../active-directory/role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="b8a67-168">了解 toomanage 與的存取方式：</span><span class="sxs-lookup"><span data-stu-id="b8a67-168">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="b8a67-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8a67-169">PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="b8a67-170">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8a67-170">Azure CLI</span></span>](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="b8a67-171">REST API</span><span class="sxs-lookup"><span data-stu-id="b8a67-171">REST API</span></span>](../active-directory/role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="b8a67-172">[角色型存取控制疑難排解](../active-directory/role-based-access-control-troubleshooting.md)︰取得修正常見問題的建議。</span><span class="sxs-lookup"><span data-stu-id="b8a67-172">[Role-Based Access Control troubleshooting](../active-directory/role-based-access-control-troubleshooting.md): Get suggestions for fixing common issues.</span></span>
