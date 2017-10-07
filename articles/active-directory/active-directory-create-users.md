---
title: "新使用者 tooAzure aaaAdd Active Directory |Microsoft 文件"
description: "說明如何 tooadd 新使用者或變更 Azure Active Directory 中的使用者資訊。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>新增使用者或與 Microsoft 帳戶 tooAzure Active Directory 使用者
新增使用者 toopopulate 您的目錄。 這篇文章說明如何 tooadd 新使用者在您的組織，以及如何 tooadd 使用者具有 Microsoft 帳戶。 如需新增來自 Azure Active Directory 中其他目錄之使用者或是來自合作夥伴公司之使用者的詳細資訊，請參閱 [新增來自 Azure Active Directory 中其他目錄或合作夥伴公司的使用者](active-directory-create-users-external.md)。 新增的使用者時，不需要系統管理員權限，根據預設，但您可以在任何時間指派角色 toothem。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 針對如何 tooadd hello Azure AD 系統管理中心中的使用者看到[加入新使用者 tooAzure Active Directory](active-directory-users-create-azure-portal.md)。

## <a name="add-a-user"></a>新增使用者
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)hello 目錄的全域管理員的帳戶。
2. 選取**Active Directory**，然後選取您的組織目錄中的 hello 名稱。
3. 選取 hello**使用者**索引標籤，然後 hello 命令列中，選取**新增使用者**。
4. 在 hello**告訴我們這位使用者**頁面的 **使用者類型**，選取：

   * **您組織中的新使用者** – 在您的目錄中新增使用者帳戶。
   * **使用現有的 Microsoft 帳戶使用者**– 新增的現有 Microsoft 消費者帳戶 tooyour 目錄 （例如 Outlook 帳戶）
5. 根據 [使用者類型] 輸入使用者名稱 (適用於新使用者) 或電子郵件地址 (適用於具有 Microsoft 帳戶的使用者)。
6. 在 hello 使用者**設定檔**頁面上，提供第一個和最後一個名稱、 使用者易記的名稱，以及使用者角色的 hello**角色**清單。 如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。 指定是否太**啟用 Multi-factor Authentication** hello 使用者。
7. 在 hello**取得暫時密碼**頁面上，選取**建立**。

> [!IMPORTANT]
> 如果您的組織使用多個網域，您應該了解 hello 新增使用者帳戶時，下列問題：
>
> * tooadd 使用者帳戶與 hello 相同的使用者主體名稱 (UPN) 跨網域，**第一個**，例如新增geoffgrisso@contoso.onmicrosoft.com，**後面** geoffgrisso@contoso.com。
> * 請「勿」先新增 geoffgrisso@contoso.com，再新增 geoffgrisso@contoso.onmicrosoft.com。這個順序很重要，而且可以麻煩 tooundo。
>
>

## <a name="change-user-information"></a>變更使用者資訊
您可以變更任何使用者屬性除了 hello 物件識別碼。

1. 開啟您的目錄。
2. 選取 hello**使用者**索引標籤，然後再選取 hello 顯示名稱 hello 想 toochange 使用者。
3. 完成您的變更，然後按一下儲存 。

如果您要變更的 hello 使用者會與您的內部部署 Active Directory 服務同步處理，您無法變更使用此程序的 hello 使用者資訊。 toochange hello 使用者，使用您在內部部署 Active Directory 管理工具。

## <a name="guest-user-management-and-limitations"></a>來賓使用者管理和限制
Guest 帳戶是從已受邀的 tooyour 目錄 tooaccess SharePoint 文件、 應用程式或其他 Azure 資源的其他目錄的使用者。 來賓帳戶在您的目錄中具有其基礎的 UserType 屬性設定太"Guest。" 一般使用者 （具體而言，您的目錄成員） 具有 hello UserType 屬性 「 成員 」。

來賓 hello 目錄中有一組有限的權限。 這些權限限制 hello 有關客體 toodiscover hello 目錄中的其他使用者的能力。 不過，來賓使用者仍然可以互動 hello 使用者與群組正努力 hello 資源相關聯。 來賓使用者可以：

* 其他使用者和群組指派給這些是 Azure 訂用帳戶 toowhich 相關聯，請參閱
* 請參閱其所屬的群組 toowhich hello 成員
* 查閱 hello 目錄中的其他使用者知道 hello 使用者 hello 完整電子郵件地址
* 請參閱僅提供有限的查閱-有限的 toodisplay 名稱、 電子郵件地址、 使用者主要名稱 (UPN) 和縮圖相片的 hello 使用者屬性
* 取得一份 hello 目錄中的已驗證網域
* 同意 tooapplications，授與他們 hello 相同目錄中有成員的存取權

## <a name="set-guest-user-access-policies"></a>設定來賓使用者存取原則
hello**設定**目錄的索引標籤包含 guest 使用者的選項 toocontrol 存取。 這些選項只可以由目錄全域管理員在 Azure 傳統入口網站中進行變更。 目前沒有透過 PowerShell 或 API 的方法。

tooopen hello**設定**] 索引標籤中 hello Azure 傳統入口網站中，選取**Active Directory**，然後選取 [hello hello 目錄名稱。

![在 Azure Active Directory 中設定索引標籤][1]

然後您可以編輯 guest 使用者的 hello 選項 toocontrol 存取。

![來賓使用者的存取控制選項][2]

## <a name="whats-next"></a>後續步驟
* [新增來自 Azure Active Directory 中其他目錄或合作夥伴公司的使用者](active-directory-create-users-external.md)
* [管理 Azure AD](active-directory-administer.md)
* [在 Azure AD 中管理密碼](active-directory-manage-passwords.md)
* [在 Azure AD 中管理群組](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
