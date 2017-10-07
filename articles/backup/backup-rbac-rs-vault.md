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
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>使用角色型存取控制 toomanage Azure 備份復原點
Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。 使用 RBAC 時，您可以隔離您的小組內的責任，並授與存取 toousers 只 hello 量他們需要 tooperform 他們的工作。

> [!IMPORTANT]
> Azure Backup 所提供角色可以在 Azure 入口網站中執行的有限的 tooactions 或復原服務保存庫的 PowerShell cmdlet。 在 Azure 備份代理程式用戶端 UI、System Center Data Protection Manager UI 或 Azure 備份伺服器 UI 中執行的動作則非這些角色所能控制。

Azure 備份提供 3 的內建角色 toocontrol 備份管理作業。 深入了解 [Azure RBAC 內建角色](../active-directory/role-based-access-built-in-roles.md)

* [備份參與者](../active-directory/role-based-access-built-in-roles.md#backup-contributor)-這個角色具有所有使用權限 toocreate 和管理備份建立復原服務保存庫，並提供存取 tooothers 除外。 您可以將此角色想做是管理備份的系統管理員，其可執行每一種備份管理作業。
* [Backup Operator](../active-directory/role-based-access-built-in-roles.md#backup-operator) -這個角色有權限 tooeverything 參與者沒有除非移除備份和管理備份原則。 這個角色是相等 toocontributor，不過它無法執行破壞性作業，例如 停止備份與刪除資料，或移除註冊的內部部署資源。
* [備份讀取器](../active-directory/role-based-access-built-in-roles.md#backup-reader)-這個角色有權限 tooview 所有備份的管理作業。 假設此角色 toobe 監視的人員。

如果您要尋找 toodefine 您自己的角色的更多控制，請參閱如何太[建置自訂角色](../active-directory/role-based-access-control-custom-roles.md)Azure rbac 進行中。



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>對應備份內建角色 toobackup 管理動作
下表中的 hello 擷取 hello 備份管理動作，並對應的最小 RBAC 角色所需 tooperform 該作業。

| 管理作業 | 所需的最小 RBAC 角色 |
| --- | --- |
| 建立復原服務保存庫 | 保存庫資源群組的參與者 |
| 啟用 Azure VM 的備份 | 在保存庫上為備份操作員，在 VM 上為虛擬機器參與者 |
| VM 的隨選備份 | 備份操作員 |
| 還原 VM | 備份操作員、 VM 和 Vnet 的資源群組參與者是持續 tooget 部署 |
| 從 VM 備份還原磁碟、個別檔案 | 備份操作員 |
| 建立 Azure VM 備份的備份原則 | 備份參與者 |
| 修改 Azure VM 備份的備份原則 | 備份參與者 |
| 刪除 Azure VM 備份的備份原則 | 備份參與者 |
| 在 VM 備份上停止備份 (保留資料或刪除資料) | 備份參與者 |
| 註冊內部部署 Windows Server/用戶端/SCDPM 或 Azure 備份伺服器 | 備份操作員 |
| 刪除已註冊的內部部署 Windows Server/用戶端/SCDPM 或 Azure 備份伺服器 | 備份參與者 |

## <a name="next-steps"></a>後續步驟
* [Role Based Access Control](../active-directory/role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。
* 了解 toomanage 與的存取方式：
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [角色型存取控制疑難排解](../active-directory/role-based-access-control-troubleshooting.md)︰取得修正常見問題的建議。
