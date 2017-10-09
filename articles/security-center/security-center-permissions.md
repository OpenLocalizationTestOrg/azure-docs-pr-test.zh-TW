---
title: "在 Azure 資訊安全中心 aaaPermissions |Microsoft 文件"
description: "這篇文章說明 Azure 資訊安全中心如何使用角色型存取控制 tooassign 權限 toousers 並找出 hello 允許每個角色的動作。"
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Azure 資訊安全中心的權限

使用 azure 資訊安全中心[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)，這樣會提供[內建角色](../active-directory/role-based-access-built-in-roles.md)toousers、 群組和服務在 Azure 中的可獲指派。

資訊安全中心會評估 hello 和組態都資源 tooidentify 安全性問題的弱點。 資訊安全中心，因此您只看到資訊相關 tooa 資源時指派資源所屬的 hello 訂用帳戶或資源群組的擁有者、 參與者或讀取器 hello 角色。

在加法 toothese 角色中，有兩個特定的資訊安全中心角色：

* **安全性讀取器**： 使用者所屬 toothis 角色有檢視權限 tooSecurity 中心。 hello 使用者可以檢視建議、 警示、 安全性原則，以及安全性狀態，但無法進行變更。
* **安全性系統管理員**： 使用者所屬 toothis 角色具有相同權限為 hello 安全性讀取器的 hello 和也更新 hello 安全性原則及關閉警示和建議。

> [!NOTE]
> hello 的安全性角色，安全讀取器和安全性系統管理員，可以存取只有在資訊安全中心。 hello 安全性角色沒有存取 tooother 服務區域的 Azure 儲存體、 Web 和行動裝置、 或物聯網等。
>
>

## <a name="roles-and-allowed-actions"></a>角色和允許的動作

hello 下表顯示角色，並允許資訊安全中心中的動作。 X 表示該角色允許 hello 動作。

| 角色 | 編輯安全性原則 | 針對資源套用安全性建議 | 關閉警示和建議 | 檢視警示和建議 |
|:--- |:---:|:---:|:---:|:---:|
| 訂用帳戶擁有者 | X | X | X | X |
| 訂用帳戶參與者 | X | X | X | X |
| 資源群組擁有者 | -- | X | -- | X |
| 資源群組參與者 | -- | X | -- | X |
| 讀取者 | -- | -- | -- | X |
| 安全性系統管理員 | X | -- | X | X |
| 安全性讀取者 | -- | -- | -- | X |

> [!NOTE]
> 我們建議您將指派 hello 最寬鬆的角色所需的使用者 toocomplete 其工作。 例如，指派 hello 讀取器角色 toousers 者只需要 tooview hello 安全性健全狀況的資訊資源，但未採取任何動作，例如套用建議，或編輯原則。
>
>

## <a name="next-steps"></a>後續步驟
這篇文章說明如何資訊安全中心使用 RBAC tooassign 權限 toousers，並識別 hello 允許每個角色的動作。 既然您已熟悉 hello 角色指派所需 toomonitor hello 的訂用帳戶的安全性狀態，編輯安全性原則，並套用建議，了解如何：

- [在資訊安全中心設定安全性原則](security-center-policies.md)
- [管理資訊安全中心的安全性建議](security-center-recommendations.md)
- [監視您的 Azure 資源 hello 安全性健全狀況](security-center-monitoring.md)
- [管理及回應 toosecurity 警示資訊安全中心](security-center-managing-and-responding-alerts.md)
- [監視合作夥伴安全性解決方案](security-center-partner-solutions.md)
