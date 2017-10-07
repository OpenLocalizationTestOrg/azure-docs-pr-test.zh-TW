---
title: "aaaDisable 使用者登入 Azure Active Directory 中的企業應用程式 |Microsoft 文件"
description: "如何 toodisable 企業應用程式，讓任何使用者可能登入 Azure Active Directory 中 tooit"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>在 Azure Active Directory 中停用企業應用程式的使用者登入
它是簡單 toodisable 企業應用程式，因此沒有任何使用者可能登入 Azure Active Directory (Azure AD) 中的 tooit。 您必須擁有 hello 適當的權限 toomanage hello 企業應用程式，，您必須是全域管理員的 hello 目錄。

## <a name="how-do-i-disable-user-sign-ins"></a>如何停用使用者登入？
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**更多服務**，輸入**Azure Active Directory**在 hello 文字方塊中，然後選取  **Enter**。
3. 在 hello **Azure Active Directory** -  ***directoryname***刀鋒視窗 （也就是 hello Azure AD 刀鋒視窗中您所管理的 hello 目錄），選取**的企業應用程式**.

    ![開啟企業應用程式](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. 在 hello**企業應用程式**刀鋒視窗中，選取**所有應用程式**。 您會看到一份可以管理的 hello 應用程式。
5. 在 hello**企業應用程式的所有應用程式**刀鋒視窗中，選取一個應用程式。
6. 在 hello ***appname***刀鋒視窗 （也就是 hello 刀鋒視窗中的 hello hello 標題中的 hello 選應用程式的名稱），選取**屬性**。

    ![選取 hello 所有應用程式的命令](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. 在 hello ***appname*** - **屬性**刀鋒視窗中，選取**否**如**toosign 中的使用者啟用？**。
8. 選取 hello**儲存**命令。

## <a name="next-steps"></a>後續步驟
* [查看我的所有群組](active-directory-groups-view-azure-portal.md)
* [指派使用者或群組的 tooan 企業應用程式](active-directory-coreapps-assign-user-azure-portal.md)
* [從企業應用程式中移除使用者或群組指派](active-directory-coreapps-remove-assignment-azure-portal.md)
* [變更 hello 名稱或企業應用程式的標誌](active-directory-coreapps-change-app-logo-user-azure-portal.md)
