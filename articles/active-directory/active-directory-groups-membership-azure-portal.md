---
title: "您的群組所屬 tooin Azure Active Directory aaaManage hello 群組 |Microsoft 文件"
description: "在 Azure Active Directory 中，群組可以包含其他群組。 以下是如何 toomanage 那些成員資格。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>管理您的 Azure Active Directory 租用戶中的群組所屬的 toowhich 群組
在 Azure Active Directory 中，群組可以包含其他群組。 以下是如何 toomanage 那些成員資格。

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>如何找到我的群組隸屬的 hello 群組？
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取 [ **Enter**。

   ![開啟使用者管理](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. 在 [hello**使用者和群組**刀鋒視窗中，選取**所有群組**。

   ![開啟 hello 群組刀鋒視窗](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. 在 [hello**使用者和群組的所有群組**刀鋒視窗中，選取一個群組。
5. 在 [hello**群組- *groupname* **刀鋒視窗中，選取**群組成員資格**。

   ![開啟 hello 群組成員資格] 刀鋒視窗](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd hello 上的另一個群組的成員身分群組**群組-群組成員資格**刀鋒視窗中，選取 hello**新增**命令。
7. 選取群組從 hello**選取群組**刀鋒視窗，，然後選取 hello**選取**在 hello hello 刀鋒視窗底部的按鈕。 您可以加入群組 tooonly 的一個群組，一次。 hello**使用者**方塊篩選 hello 顯示根據比對您的使用者或裝置名稱的項目 tooany 部分。 該方塊中不接受任何萬用字元。

   ![新增群組成員資格](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove hello 上的另一個群組的成員身分群組**群組-群組成員資格**刀鋒視窗中，選取一個群組。
9. 在 [hello ***groupname***刀鋒視窗中，選取 hello**移除**命令，然後確認您選擇在 hello 提示字元。

   ![移除成員資格命令](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. 完成變更您群組的群組成員資格時，選取 [儲存] 。

## <a name="additional-information"></a>其他資訊
這些文章提供有關 Azure Active Directory 的其他資訊。

* [查看現有的群組](active-directory-groups-view-azure-portal.md)
* [建立新群組並新增成員](active-directory-groups-create-azure-portal.md)
* [管理群組的設定](active-directory-groups-settings-azure-portal.md)
* [管理群組的成員](active-directory-groups-members-azure-portal.md)
* [管理群組中使用者的動態規則](active-directory-groups-dynamic-membership-azure-portal.md)
