---
title: "aaaView Azure 資源存取設定 |Microsoft 文件"
description: "檢視及管理的任何使用者或群組 hello Azure 入口網站中的所有 hello 角色型存取控制指派"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>檢視存取工作分派 hello Azure 入口網站中的使用者及群組
> [!div class="op_single_selector"]
> * [使用者或群組管理存取](role-based-access-control-manage-assignments.md)
> * [資源管理存取](role-based-access-control-configure.md)

您可以使用角色型存取控制 (RBAC) hello Azure Active Directory (Azure AD) 中，管理存取 tooyour Azure 資源。 

使用 RBAC 指派的存取是更細緻的因為有兩種方式，您可以限制 hello 權限：

* **範圍：** RBAC 角色指派是已設定領域的 tooa 特定訂用帳戶、 資源群組或資源。 指定存取 tooa 單一資源的使用者無法存取 hello 中的任何其他資源相同的訂用帳戶。
* **角色：**存取縮小到 hello 在範圍內的 hello 分派，甚至進一步將角色指派。 角色可為高層級，例如擁有者或特定，例如虛擬機器讀取器。

只能從 hello 訂用帳戶、 資源群組或資源，是 hello 分派 hello 範圍內指派角色。 但是，您可以在單一位置來檢視指定的使用者或群組的所有 hello 存取指派。 您可以向上 too2000 每個訂用帳戶中的角色指派。 

取得有關的詳細資訊太[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](role-based-access-control-configure.md)。

## <a name="view-access-assignments"></a>檢視存取權指派
toolook 向上 hello 存取指派單一使用者或群組，開始在 Azure Active Directory 中 hello [Azure 入口網站](http://portal.azure.com)。

1. 選取 **Azure Active Directory**。 如果此選項不是顯示在瀏覽清單上，選取**更服務**，然後捲動 toofind **Azure Active Directory**。
2. 選取 [使用者和群組]，然後選取 [所有使用者]或 [所有群組]。 在此範例中，我們將重點放在個別使用者。
    ![在 Azure Active Directory 中管理使用者和群組 - 螢幕擷取畫面](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. 依名稱或使用者名稱搜尋 hello 使用者。
4. 選取**Azure 資源**hello 使用者] 刀鋒視窗。 該使用者的所有 hello 存取指派會都出現。

### <a name="read-permissions-tooview-assignments"></a>Tooview 指派讀取權限
此頁面只會顯示 hello 存取指派您有權限 tooread。 比方說，您具有讀取權限 toosubscription A，並移 toohello Azure 資源刀鋒視窗 toocheck 使用者的指派。 您可以看到她的訂用帳戶 A 存取權指派，但無法看到她在訂用帳戶 B 上也擁有存取權指派。

## <a name="delete-access-assignments"></a>刪除存取權指派
從這個刀鋒視窗中，您可以刪除 tooa 使用者或群組直接指派的存取權指派。 如果 hello 存取指派繼承自父群組，您會需要 toogo toohello 資源或訂用帳戶和管理那里 hello 分派。

1. 從 hello 的所有 hello 存取指派使用者或群組] 清單中，選取 hello 其中一個要 toodelete。
2. 選取**移除**然後**是**tooconfirm。
    ![移除存取權指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>後續步驟

* 開始使用角色型存取控制中太[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](role-based-access-control-configure.md)
* 請參閱 hello [RBAC 內建的角色](role-based-access-built-in-roles.md)

