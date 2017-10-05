---
title: "使用 Azure 角色型存取控制管理備份 | Microsoft Docs"
description: "使用角色型存取控制來管理復原服務保存庫中的備份管理作業存取權。"
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
ms.openlocfilehash: d0b6eb8eea8971eb8f80c6623f9a41a3692241b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-role-based-access-control-to-manage-azure-backup-recovery-points"></a><span data-ttu-id="5117d-103">使用角色型存取控制來管理 Azure 備份復原點</span><span class="sxs-lookup"><span data-stu-id="5117d-103">Use Role-Based Access Control to manage Azure Backup recovery points</span></span>
<span data-ttu-id="5117d-104">Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="5117d-104">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="5117d-105">RBAC 可讓您區隔小組內的職責，而僅授與使用者執行作業所需的存取權。</span><span class="sxs-lookup"><span data-stu-id="5117d-105">Using RBAC, you can segregate duties within your team and grant only the amount of access to users that they need to perform their jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5117d-106">Azure 備份所提供的角色僅限執行可在 Azure 入口網站或復原服務保存庫 PowerShell Cmdlet 中執行的動作。</span><span class="sxs-lookup"><span data-stu-id="5117d-106">Roles provided by Azure Backup are limited to actions that can be performed in Azure portal or Recovery Services vault PowerShell cmdlets.</span></span> <span data-ttu-id="5117d-107">在 Azure 備份代理程式用戶端 UI、System Center Data Protection Manager UI 或 Azure 備份伺服器 UI 中執行的動作則非這些角色所能控制。</span><span class="sxs-lookup"><span data-stu-id="5117d-107">Actions performed in Azure backup Agent Client UI or System center Data Protection Manager UI or Azure Backup Server UI are out of control of these roles.</span></span>

<span data-ttu-id="5117d-108">Azure 備份提供 3 種用來控制備份管理作業的內建角色。</span><span class="sxs-lookup"><span data-stu-id="5117d-108">Azure Backup provides 3 built-in roles to control backup management operations.</span></span> <span data-ttu-id="5117d-109">深入了解 [Azure RBAC 內建角色](../active-directory/role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="5117d-109">Learn more on [Azure RBAC built-in roles](../active-directory/role-based-access-built-in-roles.md)</span></span>

* <span data-ttu-id="5117d-110">[備份參與者](../active-directory/role-based-access-built-in-roles.md#backup-contributor) - 此角色具有所有用來建立和管理備份的權限，但用來建立復原服務保存庫和賦予他人存取權的權限除外。</span><span class="sxs-lookup"><span data-stu-id="5117d-110">[Backup Contributor](../active-directory/role-based-access-built-in-roles.md#backup-contributor) - This role has all permissions to create and manage backup except creating Recovery Services vault and giving access to others.</span></span> <span data-ttu-id="5117d-111">您可以將此角色想做是管理備份的系統管理員，其可執行每一種備份管理作業。</span><span class="sxs-lookup"><span data-stu-id="5117d-111">Imagine this role as admin of backup management who can do every backup management operation.</span></span>
* <span data-ttu-id="5117d-112">[備份操作員](../active-directory/role-based-access-built-in-roles.md#backup-operator) - 此角色擁有參與者的所有權限，但用來移除備份和管理備份原則的權限除外。</span><span class="sxs-lookup"><span data-stu-id="5117d-112">[Backup Operator](../active-directory/role-based-access-built-in-roles.md#backup-operator) - This role has permissions to everything a contributor does except removing backup and managing backup policies.</span></span> <span data-ttu-id="5117d-113">此角色相當於參與者，但無法執行破壞性作業，例如停止備份並刪除資料，或移除內部部署資源的註冊。</span><span class="sxs-lookup"><span data-stu-id="5117d-113">This role is equivalent to contributor except it can't perform destructive operations such as stop backup with delete data or remove registration of on-premises resources.</span></span>
* <span data-ttu-id="5117d-114">[備份讀取者](../active-directory/role-based-access-built-in-roles.md#backup-reader) - 此角色擁有用來檢視所有備份管理作業的權限。</span><span class="sxs-lookup"><span data-stu-id="5117d-114">[Backup Reader](../active-directory/role-based-access-built-in-roles.md#backup-reader) - This role has permissions to view all backup management operations.</span></span> <span data-ttu-id="5117d-115">您可以將此角色想做是監視者。</span><span class="sxs-lookup"><span data-stu-id="5117d-115">Imagine this role to be a monitoring person.</span></span>

<span data-ttu-id="5117d-116">如果您想要定義自己的角色，獲得更進一步控制，請參閱如何建立 [Azure RBAC 中的自訂角色](../active-directory/role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="5117d-116">If you're looking to define your own roles for even more control, see how to [build Custom roles](../active-directory/role-based-access-control-custom-roles.md) in Azure RBAC.</span></span>



## <a name="mapping-backup-built-in-roles-to-backup-management-actions"></a><span data-ttu-id="5117d-117">將備份的內建角色對應至備份管理動作</span><span class="sxs-lookup"><span data-stu-id="5117d-117">Mapping Backup built-in roles to backup management actions</span></span>
<span data-ttu-id="5117d-118">下表會擷取備份管理動作與執行該作業所需的最小對應 RBAC 角色。</span><span class="sxs-lookup"><span data-stu-id="5117d-118">The following table captures the Backup management actions and corresponding minimum RBAC role required to perform that operation.</span></span>

| <span data-ttu-id="5117d-119">管理作業</span><span class="sxs-lookup"><span data-stu-id="5117d-119">Management Operation</span></span> | <span data-ttu-id="5117d-120">所需的最小 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="5117d-120">Minimum RBAC role required</span></span> |
| --- | --- |
| <span data-ttu-id="5117d-121">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="5117d-121">Create Recovery Services vault</span></span> | <span data-ttu-id="5117d-122">保存庫資源群組的參與者</span><span class="sxs-lookup"><span data-stu-id="5117d-122">Contributor on Resource group of vault</span></span> |
| <span data-ttu-id="5117d-123">啟用 Azure VM 的備份</span><span class="sxs-lookup"><span data-stu-id="5117d-123">Enable backup of Azure VMs</span></span> | <span data-ttu-id="5117d-124">在保存庫上為備份操作員，在 VM 上為虛擬機器參與者</span><span class="sxs-lookup"><span data-stu-id="5117d-124">Backup Operator on vault, Virtual machine contributor on VMs</span></span> |
| <span data-ttu-id="5117d-125">VM 的隨選備份</span><span class="sxs-lookup"><span data-stu-id="5117d-125">On-demand backup of VM</span></span> | <span data-ttu-id="5117d-126">備份操作員</span><span class="sxs-lookup"><span data-stu-id="5117d-126">Backup operator</span></span> |
| <span data-ttu-id="5117d-127">還原 VM</span><span class="sxs-lookup"><span data-stu-id="5117d-127">Restore VM</span></span> | <span data-ttu-id="5117d-128">VM 和 Vnet 將部署之所在位置的備份操作員和資源群組參與者</span><span class="sxs-lookup"><span data-stu-id="5117d-128">Backup operator, Resource group contributor in which VM and Vnets are going to get deployed</span></span> |
| <span data-ttu-id="5117d-129">從 VM 備份還原磁碟、個別檔案</span><span class="sxs-lookup"><span data-stu-id="5117d-129">Restore disks, individual files from VM backup</span></span> | <span data-ttu-id="5117d-130">備份操作員</span><span class="sxs-lookup"><span data-stu-id="5117d-130">Backup operator</span></span> |
| <span data-ttu-id="5117d-131">建立 Azure VM 備份的備份原則</span><span class="sxs-lookup"><span data-stu-id="5117d-131">Create backup policy for Azure VM backup</span></span> | <span data-ttu-id="5117d-132">備份參與者</span><span class="sxs-lookup"><span data-stu-id="5117d-132">Backup contributor</span></span> |
| <span data-ttu-id="5117d-133">修改 Azure VM 備份的備份原則</span><span class="sxs-lookup"><span data-stu-id="5117d-133">Modify backup policy of Azure VM backup</span></span> | <span data-ttu-id="5117d-134">備份參與者</span><span class="sxs-lookup"><span data-stu-id="5117d-134">Backup contributor</span></span> |
| <span data-ttu-id="5117d-135">刪除 Azure VM 備份的備份原則</span><span class="sxs-lookup"><span data-stu-id="5117d-135">Delete backup policy of Azure VM backup</span></span> | <span data-ttu-id="5117d-136">備份參與者</span><span class="sxs-lookup"><span data-stu-id="5117d-136">Backup contributor</span></span> |
| <span data-ttu-id="5117d-137">在 VM 備份上停止備份 (保留資料或刪除資料)</span><span class="sxs-lookup"><span data-stu-id="5117d-137">Stop backup (with retain data or delete data) on VM backup</span></span> | <span data-ttu-id="5117d-138">備份參與者</span><span class="sxs-lookup"><span data-stu-id="5117d-138">Backup contributor</span></span> |
| <span data-ttu-id="5117d-139">註冊內部部署 Windows Server/用戶端/SCDPM 或 Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="5117d-139">Register on-premises Windows Server/client/SCDPM or Azure Backup Server</span></span> | <span data-ttu-id="5117d-140">備份操作員</span><span class="sxs-lookup"><span data-stu-id="5117d-140">Backup operator</span></span> |
| <span data-ttu-id="5117d-141">刪除已註冊的內部部署 Windows Server/用戶端/SCDPM 或 Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="5117d-141">Delete registered on-premises Windows Server/client/SCDPM or Azure Backup Server</span></span> | <span data-ttu-id="5117d-142">備份參與者</span><span class="sxs-lookup"><span data-stu-id="5117d-142">Backup contributor</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5117d-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5117d-143">Next steps</span></span>
* <span data-ttu-id="5117d-144">[角色型存取控制](../active-directory/role-based-access-control-configure.md)：開始在 Azure 入口網站中使用 RBAC。</span><span class="sxs-lookup"><span data-stu-id="5117d-144">[Role Based Access Control](../active-directory/role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="5117d-145">了解如何使用下列各項管理存取權：</span><span class="sxs-lookup"><span data-stu-id="5117d-145">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="5117d-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5117d-146">PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="5117d-147">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5117d-147">Azure CLI</span></span>](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="5117d-148">REST API</span><span class="sxs-lookup"><span data-stu-id="5117d-148">REST API</span></span>](../active-directory/role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="5117d-149">[角色型存取控制疑難排解](../active-directory/role-based-access-control-troubleshooting.md)︰取得修正常見問題的建議。</span><span class="sxs-lookup"><span data-stu-id="5117d-149">[Role-Based Access Control troubleshooting](../active-directory/role-based-access-control-troubleshooting.md): Get suggestions for fixing common issues.</span></span>
