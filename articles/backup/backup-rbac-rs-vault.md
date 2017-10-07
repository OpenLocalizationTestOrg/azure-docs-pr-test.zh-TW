---
title: "使用 Azure 角色型存取控制管理備份 | Microsoft Docs"
description: "復原服務保存庫中使用角色型存取控制 toomanage 存取 toobackup 管理作業。"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a><span data-ttu-id="bf661-103">使用角色型存取控制 toomanage Azure 備份復原點</span><span class="sxs-lookup"><span data-stu-id="bf661-103">Use Role-Based Access Control toomanage Azure Backup recovery points</span></span>
<span data-ttu-id="bf661-104">Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="bf661-104">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="bf661-105">使用 RBAC 時，您可以隔離您的小組內的責任，並授與存取 toousers 只 hello 量他們需要 tooperform 他們的工作。</span><span class="sxs-lookup"><span data-stu-id="bf661-105">Using RBAC, you can segregate duties within your team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf661-106">Azure Backup 所提供角色可以在 Azure 入口網站中執行的有限的 tooactions 或復原服務保存庫的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bf661-106">Roles provided by Azure Backup are limited tooactions that can be performed in Azure portal or Recovery Services vault PowerShell cmdlets.</span></span> <span data-ttu-id="bf661-107">在 Azure 備份代理程式用戶端 UI、System Center Data Protection Manager UI 或 Azure 備份伺服器 UI 中執行的動作則非這些角色所能控制。</span><span class="sxs-lookup"><span data-stu-id="bf661-107">Actions performed in Azure backup Agent Client UI or System center Data Protection Manager UI or Azure Backup Server UI are out of control of these roles.</span></span>

<span data-ttu-id="bf661-108">Azure 備份提供 3 的內建角色 toocontrol 備份管理作業。</span><span class="sxs-lookup"><span data-stu-id="bf661-108">Azure Backup provides 3 built-in roles toocontrol backup management operations.</span></span> <span data-ttu-id="bf661-109">深入了解 [Azure RBAC 內建角色](../active-directory/role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="bf661-109">Learn more on [Azure RBAC built-in roles](../active-directory/role-based-access-built-in-roles.md)</span></span>

* <span data-ttu-id="bf661-110">[備份參與者](../active-directory/role-based-access-built-in-roles.md#backup-contributor)-這個角色具有所有使用權限 toocreate 和管理備份建立復原服務保存庫，並提供存取 tooothers 除外。</span><span class="sxs-lookup"><span data-stu-id="bf661-110">[Backup Contributor](../active-directory/role-based-access-built-in-roles.md#backup-contributor) - This role has all permissions toocreate and manage backup except creating Recovery Services vault and giving access tooothers.</span></span> <span data-ttu-id="bf661-111">您可以將此角色想做是管理備份的系統管理員，其可執行每一種備份管理作業。</span><span class="sxs-lookup"><span data-stu-id="bf661-111">Imagine this role as admin of backup management who can do every backup management operation.</span></span>
* <span data-ttu-id="bf661-112">[Backup Operator](../active-directory/role-based-access-built-in-roles.md#backup-operator) -這個角色有權限 tooeverything 參與者沒有除非移除備份和管理備份原則。</span><span class="sxs-lookup"><span data-stu-id="bf661-112">[Backup Operator](../active-directory/role-based-access-built-in-roles.md#backup-operator) - This role has permissions tooeverything a contributor does except removing backup and managing backup policies.</span></span> <span data-ttu-id="bf661-113">這個角色是相等 toocontributor，不過它無法執行破壞性作業，例如 停止備份與刪除資料，或移除註冊的內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="bf661-113">This role is equivalent toocontributor except it can't perform destructive operations such as stop backup with delete data or remove registration of on-premises resources.</span></span>
* <span data-ttu-id="bf661-114">[備份讀取器](../active-directory/role-based-access-built-in-roles.md#backup-reader)-這個角色有權限 tooview 所有備份的管理作業。</span><span class="sxs-lookup"><span data-stu-id="bf661-114">[Backup Reader](../active-directory/role-based-access-built-in-roles.md#backup-reader) - This role has permissions tooview all backup management operations.</span></span> <span data-ttu-id="bf661-115">假設此角色 toobe 監視的人員。</span><span class="sxs-lookup"><span data-stu-id="bf661-115">Imagine this role toobe a monitoring person.</span></span>

<span data-ttu-id="bf661-116">如果您要尋找 toodefine 您自己的角色的更多控制，請參閱如何太[建置自訂角色](../active-directory/role-based-access-control-custom-roles.md)Azure rbac 進行中。</span><span class="sxs-lookup"><span data-stu-id="bf661-116">If you're looking toodefine your own roles for even more control, see how too[build Custom roles](../active-directory/role-based-access-control-custom-roles.md) in Azure RBAC.</span></span>



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a><span data-ttu-id="bf661-117">對應備份內建角色 toobackup 管理動作</span><span class="sxs-lookup"><span data-stu-id="bf661-117">Mapping Backup built-in roles toobackup management actions</span></span>
<span data-ttu-id="bf661-118">下表中的 hello 擷取 hello 備份管理動作，並對應的最小 RBAC 角色所需 tooperform 該作業。</span><span class="sxs-lookup"><span data-stu-id="bf661-118">hello following table captures hello Backup management actions and corresponding minimum RBAC role required tooperform that operation.</span></span>

| <span data-ttu-id="bf661-119">管理作業</span><span class="sxs-lookup"><span data-stu-id="bf661-119">Management Operation</span></span> | <span data-ttu-id="bf661-120">所需的最小 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="bf661-120">Minimum RBAC role required</span></span> |
| --- | --- |
| <span data-ttu-id="bf661-121">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="bf661-121">Create Recovery Services vault</span></span> | <span data-ttu-id="bf661-122">保存庫資源群組的參與者</span><span class="sxs-lookup"><span data-stu-id="bf661-122">Contributor on Resource group of vault</span></span> |
| <span data-ttu-id="bf661-123">啟用 Azure VM 的備份</span><span class="sxs-lookup"><span data-stu-id="bf661-123">Enable backup of Azure VMs</span></span> | <span data-ttu-id="bf661-124">在保存庫上為備份操作員，在 VM 上為虛擬機器參與者</span><span class="sxs-lookup"><span data-stu-id="bf661-124">Backup Operator on vault, Virtual machine contributor on VMs</span></span> |
| <span data-ttu-id="bf661-125">VM 的隨選備份</span><span class="sxs-lookup"><span data-stu-id="bf661-125">On-demand backup of VM</span></span> | <span data-ttu-id="bf661-126">備份操作員</span><span class="sxs-lookup"><span data-stu-id="bf661-126">Backup operator</span></span> |
| <span data-ttu-id="bf661-127">還原 VM</span><span class="sxs-lookup"><span data-stu-id="bf661-127">Restore VM</span></span> | <span data-ttu-id="bf661-128">備份操作員、 VM 和 Vnet 的資源群組參與者是持續 tooget 部署</span><span class="sxs-lookup"><span data-stu-id="bf661-128">Backup operator, Resource group contributor in which VM and Vnets are going tooget deployed</span></span> |
| <span data-ttu-id="bf661-129">從 VM 備份還原磁碟、個別檔案</span><span class="sxs-lookup"><span data-stu-id="bf661-129">Restore disks, individual files from VM backup</span></span> | <span data-ttu-id="bf661-130">備份操作員</span><span class="sxs-lookup"><span data-stu-id="bf661-130">Backup operator</span></span> |
| <span data-ttu-id="bf661-131">建立 Azure VM 備份的備份原則</span><span class="sxs-lookup"><span data-stu-id="bf661-131">Create backup policy for Azure VM backup</span></span> | <span data-ttu-id="bf661-132">備份參與者</span><span class="sxs-lookup"><span data-stu-id="bf661-132">Backup contributor</span></span> |
| <span data-ttu-id="bf661-133">修改 Azure VM 備份的備份原則</span><span class="sxs-lookup"><span data-stu-id="bf661-133">Modify backup policy of Azure VM backup</span></span> | <span data-ttu-id="bf661-134">備份參與者</span><span class="sxs-lookup"><span data-stu-id="bf661-134">Backup contributor</span></span> |
| <span data-ttu-id="bf661-135">刪除 Azure VM 備份的備份原則</span><span class="sxs-lookup"><span data-stu-id="bf661-135">Delete backup policy of Azure VM backup</span></span> | <span data-ttu-id="bf661-136">備份參與者</span><span class="sxs-lookup"><span data-stu-id="bf661-136">Backup contributor</span></span> |
| <span data-ttu-id="bf661-137">在 VM 備份上停止備份 (保留資料或刪除資料)</span><span class="sxs-lookup"><span data-stu-id="bf661-137">Stop backup (with retain data or delete data) on VM backup</span></span> | <span data-ttu-id="bf661-138">備份參與者</span><span class="sxs-lookup"><span data-stu-id="bf661-138">Backup contributor</span></span> |
| <span data-ttu-id="bf661-139">註冊內部部署 Windows Server/用戶端/SCDPM 或 Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="bf661-139">Register on-premises Windows Server/client/SCDPM or Azure Backup Server</span></span> | <span data-ttu-id="bf661-140">備份操作員</span><span class="sxs-lookup"><span data-stu-id="bf661-140">Backup operator</span></span> |
| <span data-ttu-id="bf661-141">刪除已註冊的內部部署 Windows Server/用戶端/SCDPM 或 Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="bf661-141">Delete registered on-premises Windows Server/client/SCDPM or Azure Backup Server</span></span> | <span data-ttu-id="bf661-142">備份參與者</span><span class="sxs-lookup"><span data-stu-id="bf661-142">Backup contributor</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bf661-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf661-143">Next steps</span></span>
* <span data-ttu-id="bf661-144">[Role Based Access Control](../active-directory/role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="bf661-144">[Role Based Access Control](../active-directory/role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="bf661-145">了解 toomanage 與的存取方式：</span><span class="sxs-lookup"><span data-stu-id="bf661-145">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="bf661-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf661-146">PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="bf661-147">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bf661-147">Azure CLI</span></span>](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="bf661-148">REST API</span><span class="sxs-lookup"><span data-stu-id="bf661-148">REST API</span></span>](../active-directory/role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="bf661-149">[角色型存取控制疑難排解](../active-directory/role-based-access-control-troubleshooting.md)︰取得修正常見問題的建議。</span><span class="sxs-lookup"><span data-stu-id="bf661-149">[Role-Based Access Control troubleshooting](../active-directory/role-based-access-control-troubleshooting.md): Get suggestions for fixing common issues.</span></span>
