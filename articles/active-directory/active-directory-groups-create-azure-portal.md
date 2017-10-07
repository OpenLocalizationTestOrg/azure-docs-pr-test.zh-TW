---
title: "Azure Active Directory 中的使用者群組 aaaCreate |Microsoft 文件"
description: "如何 toocreate Azure Active Directory 中的群組，並加入成員 toohello 群組"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>在 Azure Active Directory 中建立群組和新增使用者
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-groups-create-azure-portal.md)
> * [Azure 傳統入口網站](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

這篇文章說明如何 toocreate 並填入 Azure Active Directory 中的新群組。 使用群組 tooperform 管理工作，例如指派授權或權限的使用者或裝置的 tooa 數次。

## <a name="how-do-i-create-a-group"></a>如何建立群組？
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。

   ![開啟使用者管理](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. 在 hello**使用者和群組**刀鋒視窗中，選取**所有群組**。

   ![開啟 hello 群組刀鋒視窗](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. 在 hello**使用者和群組的所有群組**刀鋒視窗中，選取 hello**新增**命令。

   ![選取 hello Add 命令](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. 在 hello**群組**刀鋒視窗中，加入名稱與 hello 群組的描述。
6. tooselect 成員 tooadd toohello 群組中，選取**指派**在 hello**成員資格類型**方塊，並選取**成員**。 如需有關如何 toomanage hello 群組成員資格以動態方式的詳細資訊，請參閱[使用屬性 toocreate 進階規則群組的成員資格](active-directory-groups-dynamic-membership-azure-portal.md)。

   ![選取成員 tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. 在 hello**成員**刀鋒視窗中，選取其中一個或多個使用者或裝置 tooadd toohello 群組則選取 hello**選取**按鈕在 hello 底部 hello 刀鋒視窗 tooadd 它們 toohello 群組。 hello**使用者**方塊篩選 hello 顯示根據比對您的使用者或裝置名稱的項目 tooany 部分。 該方塊中不接受任何萬用字元。
8. 當您完成新增成員 toohello 群組時，選取**建立**上 hello**群組**刀鋒視窗。    

   ![建立群組確認](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>後續步驟
這些文章提供有關 Azure Active Directory 的其他資訊。

* [查看現有的群組](active-directory-groups-view-azure-portal.md)
* [管理群組的設定](active-directory-groups-settings-azure-portal.md)
* [管理群組的成員](active-directory-groups-members-azure-portal.md)
* [管理群組的成員資格](active-directory-groups-membership-azure-portal.md)
* [管理群組中使用者的動態規則](active-directory-groups-dynamic-membership-azure-portal.md)
