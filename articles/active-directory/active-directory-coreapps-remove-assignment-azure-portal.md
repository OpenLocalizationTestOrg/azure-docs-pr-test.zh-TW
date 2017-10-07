---
title: "從 Azure Active Directory 中的企業應用程式的使用者或群組指派 aaaRemove |Microsoft 文件"
description: "Tooremove hello 從 Azure Active Directory 中的企業應用程式所存取的使用者或群組指派"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>在 Azure Active Directory 中從企業應用程式移除使用者或群組指派
它是簡單 tooremove 使用者或群組指派存取 tooone 企業應用程式在 Azure Active Directory (Azure AD) 中。 您必須擁有 hello 適當的權限 toomanage hello 企業應用程式，，您必須是全域管理員的 hello 目錄。

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>如何移除使用者或群組指派？
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**更多服務**，輸入**Azure Active Directory**在 hello 文字方塊中，然後選取  **Enter**。
3. 在 hello **Azure Active Directory- *directoryname*** 刀鋒視窗 （也就是 hello Azure AD 刀鋒視窗中您所管理的 hello 目錄），選取**企業應用程式**。

    ![開啟企業應用程式](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. 在 hello**企業應用程式**刀鋒視窗中，選取**所有應用程式**。 您會看到一份可以管理的 hello 應用程式。
5. 在 hello**企業應用程式的所有應用程式**刀鋒視窗中，選取一個應用程式。
6. 在 hello ***appname***刀鋒視窗 （也就是 hello 刀鋒視窗中的 hello hello 標題中的 hello 選應用程式的名稱），選取**使用者和群組**。

    ![選取使用者或群組](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. 在 hello ***appname*** **-使用者和群組指派**刀鋒視窗中，選取其中一個更多的使用者或群組，然後選取 hello**移除**命令。 確認您的決定在 hello 提示字元。

    ![選取 hello Remove 命令](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>後續步驟
* [查看我的所有群組](active-directory-groups-view-azure-portal.md)
* [指派使用者或群組的 tooan 企業應用程式](active-directory-coreapps-assign-user-azure-portal.md)
* [停用企業應用程式的使用者登入](active-directory-coreapps-disable-app-azure-portal.md)
* [變更 hello 名稱或企業應用程式的標誌](active-directory-coreapps-change-app-logo-user-azure-portal.md)
