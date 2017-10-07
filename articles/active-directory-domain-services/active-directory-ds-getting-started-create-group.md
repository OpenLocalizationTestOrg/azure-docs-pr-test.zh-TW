---
title: "Azure Active Directory 網域服務： 建立 hello Azure AD DC administrators 群組 |Microsoft 文件"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站
本文說明，並逐步引導您 tooenable Azure Active Directory 網域服務 (Azure AD DS) Azure Active Directory (Azure AD) 租用戶的 hello 組態工作。

> [!NOTE]
> [**請改嘗試 hello 新 Azure （預覽） 入口網站體驗**](active-directory-ds-getting-started.md)。 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>工作 1： 建立 hello Azure AD DC administrators 群組
hello 第一項工作是 toocreate Azure AD 租用戶中的系統管理群組。 這個特殊的系統管理群組稱為 *AAD DC 系統管理員*。 系統管理員權限的電腦已加入網域的 toohello Azure Active Directory 網域服務管理的網域，會授與此群組的成員。 已加入網域的電腦上，此群組會加入 toohello administrators 群組。 此外，此群組的成員可以使用遠端桌面 tooconnect 遠端 toodomain 加入機器。  

> [!NOTE]
> 您沒有 hello 您使用 Azure Active Directory 網域服務建立的受管理網域的網域系統管理員或企業系統管理員權限。 上受管理的網域，這些權限所保留的 hello 服務，並不會使用 toousers hello 租用戶中。 不過，您可以使用特殊 hello 建立系統管理群組中此組態工作 tooperform 某些特殊權限操作。 這些作業包括加入電腦 toohello 網域屬於 toohello 管理群組已加入網域的機器上，設定群組原則。
>

在這項組態工作，您可以建立 hello 系統管理群組和目錄 toohello 群組中加入一個或多個使用者。 Azure Active Directory 網域服務，toocreate hello 系統管理群組 hello 遵循：

1. 移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左窗格中，選取 [hello **Active Directory** ] 按鈕。
3. 選取 hello Azure AD 租用戶 （目錄），您會想 tooenable Azure Active Directory 網域服務。 您只能針對每個 Azure AD 目錄建立一個網域。

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. 在 [hello**預覽目錄**頁面上，按一下 hello**群組**] 索引標籤。
5. tooadd 群組 tooyour Azure AD 租用戶，在 hello hello 視窗底部的 hello 工作窗格上按一下**加入群組**。

    ![hello 加入群組 按鈕](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. 在 hello**加入群組**對話方塊方塊中，建立名為群組**AAD DC 管理員**，然後設定**群組類型**太**安全性**。

   > [!WARNING]
   > tooenable 存取 Azure Active Directory 網域服務受管理網域內建立完全同名的群組。
   >
   >

    ![hello 新增群組對話方塊](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. 在 hello**描述**方塊中，輸入描述，可讓其他人 toounderstand 此群組授與 Azure Active Directory 網域服務的系統管理權限。
8. 在您建立 hello 群組後，按一下 hello 群組名稱 tooview 其內容。
9. 為在 hello hello 視窗底部的 hello 群組成員的 tooadd 使用者按一下 hello**新增成員** 按鈕。

    ![新增群組成員按鈕](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. 在 [hello**將成員加入**對話方塊中，選取 hello 使用者應該是此群組的成員，然後按一下hello] 核取記號圖示，hello 右下。

    ![新增使用者 tooadministrators 群組](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>後續步驟
[工作 2：建立或選取 Azure 虛擬網路](active-directory-ds-getting-started-vnet.md)
