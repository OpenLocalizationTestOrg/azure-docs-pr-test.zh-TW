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
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>使用角色型存取控制 toomanage Azure Site Recovery 部署

Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。 使用 RBAC 時，您可以隔離您的小組內的責任，並授與僅特定存取權限 toousers 需要的 tooperform 特定工作的形式。

Azure Site Recovery 提供 3 的內建角色 toocontrol Site Recovery 管理作業。 深入了解 [Azure RBAC 內建角色](../active-directory/role-based-access-built-in-roles.md)

* [站台復原參與者](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor)-這個角色具有所有使用權限必要的 toomanage Azure Site Recovery 作業復原服務保存庫中。 使用者與此角色，不過，無法建立或刪除復原服務保存庫或指派存取權限 tooother 使用者。 此角色最適合用於災害復原的系統管理員可以啟用和管理的應用程式或整個組織，嚴重損壞修復作為可能 hello 案例。
* [站台復原操作員](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator)-這個角色有權限 tooexecute 和管理員容錯移轉和容錯回復作業。 具有此角色的使用者無法啟用或停用複寫，建立或刪除保存庫，註冊新的基礎結構或指派存取權限 tooother 使用者。 此角色最適合災害復原操作員，當應用程式擁有者和 IT 系統管理員在實際或模擬災害情況 (例如災害復原演習) 中指示時，操作員可以對虛擬機器或應用程式進行容錯移轉。 Post hello 災害的解析度，hello DR 運算子可以重新保護和容錯回復 hello 虛擬機器。
* [站台復原的讀取器](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader)-這個角色有權限 tooview 站台復原的所有管理作業。 這個角色是保護的適用於 IT 監視主管人員可以監視 hello 的目前狀態，並引發支援票證，必要的。

如果您要尋找 toodefine 您自己的角色的更多控制，請參閱如何太[建置自訂角色](../active-directory/role-based-access-control-custom-roles.md)在 Azure 中。

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>TooEnable 複寫所需的新虛擬機器權限
使用 Azure Site Recovery 的複寫的 tooAzure 新的虛擬機器時，相關聯的 hello 使用者的存取層級是 hello 使用者的驗證的 tooensure hello 具有必要權限 toouse hello Azure 提供的資源 tooSite 復原。

新的虛擬機器的 tooenable 複寫，使用者必須具備：
* 權限 toocreate hello 選取的資源群組中的虛擬機器
* 權限 toocreate hello 選取的虛擬網路中的虛擬機器
* 權限 toowrite toohello 選取儲存體帳戶

使用者需要下列權限 toocomplete 複寫新的虛擬機器的 hello。

> [!IMPORTANT]
>請確認相關的權限會新增每個 hello 部署模型 (資源管理員 / 傳統) 資源部署所用的。

| **資源類型** | **部署模型** | **權限** |
| --- | --- | --- |
| 計算 | 資源管理員 | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | 傳統 | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| 網路 | 資源管理員 | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | 傳統 | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| 儲存體 | 資源管理員 | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | 傳統 | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| 資源群組 | 資源管理員 | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

請考慮使用 hello '虛擬機器參與者' 和 '傳統虛擬機器參與者'[內建角色](../active-directory/role-based-access-built-in-roles.md)資源管理員] 和 [傳統部署模型分別。

## <a name="next-steps"></a>後續步驟
* [角色型存取控制](../active-directory/role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。
* 了解 toomanage 與的存取方式：
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [角色型存取控制疑難排解](../active-directory/role-based-access-control-troubleshooting.md)︰取得修正常見問題的建議。
