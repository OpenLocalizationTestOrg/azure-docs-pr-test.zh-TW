---
title: "aaaShare Azure 入口網站的儀表板使用 RBAC |Microsoft 文件"
description: "本文說明 tooshare 儀表板中的 hello Azure 入口網站使用以角色為基礎的存取控制的方式。"
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>使用角色型存取控制來共用 Azure 儀表板
設定儀表板之後，您可以將它發佈，並與組織中的其他使用者共用。 允許其他人 tooview 透過 Azure 儀表板[角色型存取控制](../active-directory/role-based-access-control-configure.md)。 您指派使用者或群組的使用者 tooa 角色，而該角色定義這些使用者可以檢視或修改 hello 已發行的儀表板。 

所有已發佈的儀表板會實作為 Azure 資源，這表示它們是做為您訂用帳戶內可管理的項目而存在，並且會包含在資源群組中。  從存取控制的觀點來看，儀表板與其他資源 (例如虛擬機器或儲存體帳戶) 並無不同。

> [!TIP]
> 個別的圖格 hello 儀表板上強制執行自己根據它們顯示 hello 資源的存取控制需求。  因此，您可以設計 hello 個別的磚上的資料仍受到保護時廣泛共用的儀表板。
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>了解儀表板的存取控制
使用角色型存取控制 (RBAC)，您可以指派使用者 tooroles 三個不同的範圍層級：

* 訂用帳戶
* 資源群組
* resource

您指派的 hello 權限被繼承自 toohello 資源下的訂用帳戶。 hello 已發行的儀表板是資源。 因此，您可能已經有 hello 訂用帳戶的使用者指派 tooroles 這也適用於 hello 已發行的儀表板。 

範例如下。  假設您有 Azure 訂用帳戶，並已指派不同的成員，您的小組 hello 角色**擁有者**，**參與者**，或**讀取器**hello 訂用帳戶。 使用者是擁有者或參與者都可以 toolist，檢視、 建立、 修改或刪除儀表板 hello 訂用帳戶內。  讀取器的使用者都能 toolist 和檢視儀表板，但無法修改或刪除它們。  讀取器存取的使用者都能 toomake 本機編輯 tooa 發行儀表板 (例如，對問題進行疑難排解時)，但您不能 toopublish 這些變更後 toohello 伺服器。  將自己擁有 hello 選項 toomake hello 儀表板的私用複本

不過，您也可以指派包含數個儀表板或 tooan 個別儀表板的權限 toohello 資源群組。 例如，您可能會決定，一群使用者應具有有限的權限跨 hello 訂用帳戶，但大於存取 tooa 特定儀表板。 您指派這些使用者 tooa 角色，該儀表板。 

## <a name="publish-dashboard"></a>發佈儀表板
讓我們假設您已完成設定您想 tooshare 要與使用者群組之前，您的訂用帳戶中的儀表板。 hello 步驟描繪一個稱為 「 存放裝置管理員的自訂的群組，但您可以命名您的群組您想要的任何內容。 如需建立 Active Directory 群組並加入使用者 toothat 群組資訊，請參閱[管理 Azure Active Directory 中的群組](../active-directory/active-directory-accessmanagement-manage-groups.md)。

1. 在 hello 儀表板中，選取 **共用**。
   
     ![選取共用](./media/azure-portal-dashboard-share-access/select-share.png)
2. 再指派存取權，您必須發佈 hello 儀表板。 根據預設，hello 儀表板將會發行的 tooa 資源群組名稱**儀表板**。 選取 [發佈] 。
   
     ![publish](./media/azure-portal-dashboard-share-access/publish.png)

儀表板現已發佈。 如果適合 hello 繼承自 hello 訂用帳戶的權限，您不需要 toodo 任何資料。 您組織中的其他使用者將會無法 tooaccess 並修改其訂用帳戶層級的角色為基礎的 hello 儀表板。 不過，本教學課程，讓我們指定使用者 tooa 角色，該儀表板的群組。

## <a name="assign-access-tooa-dashboard"></a>指派存取 tooa 儀表板
1. 發行之後 hello 儀表板，選取**管理使用者**。
   
     ![管理使用者](./media/azure-portal-dashboard-share-access/manage-users.png)
2. 您會看到已對其指派此儀表板角色的現有使用者清單。 您的現有使用者清單會不同於下面的 hello 影像。 最可能的原因 hello 分派被繼承自 hello 訂用帳戶。 tooadd 新的使用者或群組，請選取**新增**。
   
     ![新增使用者](./media/azure-portal-dashboard-share-access/existing-users.png)
3. 選取代表您想要 toogrant hello 權限的 hello 角色。 在此範例中，請選取 [參與者] 。
   
     ![選取角色](./media/azure-portal-dashboard-share-access/select-role.png)
4. 選取 hello 使用者或群組，您會希望 tooassign toohello 角色。 如果您看不 hello 使用者或群組，您要尋找 hello 清單中，使用 hello [搜尋] 方塊。 您可以使用群組的清單取決於您建立 Active Directory 中的 hello 群組。
   
     ![選取使用者](./media/azure-portal-dashboard-share-access/select-user.png) 
5. 使用者或群組新增完成時，請選取 [確定] 。 
6. hello 新作業加入 toohello 使用者清單。 請注意，其**存取權**會列為 [已指派] 而非 [已繼承]。
   
     ![指派的角色](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>後續步驟
* 如需角色清單，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。
* toolearn 關於管理資源，請參閱[透過入口網站管理 Azure 資源](resource-group-portal.md)。

