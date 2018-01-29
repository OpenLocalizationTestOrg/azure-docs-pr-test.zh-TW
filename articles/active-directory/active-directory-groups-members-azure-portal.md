---
title: "在 Azure Active Directory 中管理群組的成員 | Microsoft Docs"
description: "如何在 Azure Active Directory 的群組中新增或移除使用者和裝置"
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 49c975aa34f28c6c00591435726e538bb79a78cb
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>管理 Azure Active Directory 租用戶中使用者的群組成員資格
本文說明如何在 Azure Active Directory (Azure AD) 中管理群組的成員。

## <a name="how-do-i-find-the-members-and-manage-them"></a>如何尋找成員及管理這些成員？
1. 使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。
2. 選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。

   ![開啟使用者管理](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. 在 [使用者和群組] 刀鋒視窗上，選取 [所有群組]。

   ![開啟群組刀鋒視窗](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. 在 [使用者和群組 - 所有群組]  刀鋒視窗上，選取一個群組。
5. 在 [群組- *groupname*] 刀鋒視窗上，選取 [成員]。

   ![開啟 [成員] 刀鋒視窗](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. 若要將成員新增到群組中，請在 [群組 - 成員] 刀鋒視窗上，選取 [新增成員]。

   ![[新增成員] 命令](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. 在 [成員] 刀鋒視窗上，選取一或多個要新增到群組中的使用者或裝置，然後選取刀鋒視窗底部的 [選取] 按鈕來將它們新增到群組中。 [使用者]  方塊會根據將您的輸入內容與使用者或裝置名稱的任何部分進行比對來篩選顯示。 該方塊中不接受任何萬用字元。
8. 若要從群組中移除成員，請在 [群組 - 成員]  刀鋒視窗上，選取一個成員。
9. 在 [***membername***] 刀鋒視窗上，選取 [移除] 命令，並在出現提示時確認您的選擇。

   ![[移除成員] 命令](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. 完成變更群組的成員時，選取 [儲存] 。

## <a name="additional-information"></a>其他資訊
這些文章提供有關 Azure Active Directory 的其他資訊。

* [查看現有的群組](active-directory-groups-view-azure-portal.md)
* [建立新群組並新增成員](active-directory-groups-create-azure-portal.md)
* [管理群組的設定](active-directory-groups-settings-azure-portal.md)
* [管理群組的成員資格](active-directory-groups-membership-azure-portal.md)
* [管理群組中使用者的動態規則](active-directory-groups-dynamic-membership-azure-portal.md)
