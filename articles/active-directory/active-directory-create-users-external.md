---
title: "從其他目錄或 Azure Active Directory 中的夥伴公司 aaaAdd 使用者 |Microsoft 文件"
description: "說明如何 tooadd 使用者或變更在 Azure Active Directory，包括外部和來賓使用者的使用者資訊。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>新增來自 Azure Active Directory 中其他目錄或合作夥伴公司的使用者

這篇文章說明如何從 Azure Active Directory 中的其他目錄 tooadd 使用者或從夥伴公司中新增使用者。 如需在組織中，加入新使用者以及加入具有 Microsoft 帳戶的使用者資訊，請參閱[加入新使用者 tooAzure Active Directory](active-directory-create-users.md)。 

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 如何置 tooadd B2B 共同作業 guest 使用者，在 hello Azure AD 系統管理員中的，請參閱[什麼是 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)

新增的使用者時，不需要系統管理員權限，根據預設，但您可以在任何時間指派角色 toothem。

## <a name="add-a-user"></a>新增使用者
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)hello 目錄的全域管理員的帳戶。
2. 選取 [Active Directory] ，然後開啟您的目錄。
3. 選取 hello**使用者**索引標籤，然後 hello 命令列中，選取**新增使用者**。
4. 在 hello**告訴我們這位使用者**頁面的 **使用者類型**，選取：

   * **另一個 Azure AD 目錄中的使用者**– 將其他 Azure AD 目錄的使用者帳戶 tooyour 目錄做為來源。 只有在您也是另一個目錄的成員時，才能選取該目錄中的使用者。
   * **合作夥伴公司中的使用者**-tooinvite 並授權協力廠商公司使用者 tooyour 目錄 (請參閱[Azure Active Directory B2B 共同作業](active-directory-b2b-what-is-azure-ad-b2b.md))。 您必須太[上傳 CSV 檔案指定電子郵件地址](active-directory-b2b-references-csv-file-format.md)。
5. 在 hello 使用者**設定檔**頁面上，提供第一個和最後一個名稱、 使用者易記的名稱，以及使用者角色的 hello**角色**清單。 如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。 指定是否太**啟用 Multi-factor Authentication** hello 使用者。
6. 在 hello**取得暫時密碼**頁面上，選取**建立**。

> [!IMPORTANT]
> 如果您的組織使用多個網域，您應該了解 hello 新增使用者帳戶時，下列問題：
>
> * tooadd 使用者帳戶與 hello 相同的使用者主體名稱 (UPN) 跨網域，**第一個**，例如新增geoffgrisso@contoso.onmicrosoft.com，**後面** geoffgrisso@contoso.com。
> * 請「勿」先新增 geoffgrisso@contoso.com，再新增 geoffgrisso@contoso.onmicrosoft.com。
>

如果您變更與您在內部部署 Active Directory 服務同步處理身分識別使用者的資訊，您無法變更 hello hello Azure 傳統入口網站中的使用者資訊。 toochange hello 使用者資訊，請使用您在內部部署 Active Directory 管理工具。

## <a name="add-external-users"></a>新增外部使用者
您也可以新增使用者從您所隸屬的另一個 Azure AD 目錄 toowhich 或合作夥伴公司所上傳 CSV 檔案。 tooadd 外部使用者，如**使用者類型**，指定**另一個 Microsoft Azure AD 目錄中的使用者**或**夥伴公司中的使用者**。

這兩種類型的使用者是源自另一個目錄，並且新增為 [外部使用者] 。 外部使用者可以共同作業與其他使用者在目錄中沒有任何需求 tooadd 新帳戶和認證。 當它們登入，而該驗證也適用於已加入的任何其他目錄 toowhich 外部使用者向其主目錄中。

## <a name="external-user-management-and-limitations"></a>外部使用者管理和限制
當您從另一個目錄 tooyour 目錄新增使用者時，該使用者是您目錄中的外部使用者。 hello 顯示名稱和使用者名稱已從其主目錄複製，並使用您的目錄中的 hello 外部使用者。 從那時起，hello 外部使用者帳戶的內容是完全獨立的。 如果屬性的變更 toohello 使用者主目錄中，這些變更未傳播 toohello 外部使用者帳戶，在您的目錄。

hello hello 兩個帳戶之間的唯一連結就是針對其主目錄或其 Microsoft 帳戶，一律會驗證該 hello 使用者。 這就是為什麼您沒有看見選項 tooreset hello 密碼或啟用多因素驗證，這樣外部使用者。 目前，hello hello 主目錄或 Microsoft 帳戶的驗證原則是只有一個 hello 使用者登入時會評估 hello。

> [!NOTE]
> 您仍可停用 hello hello 目錄，它會封鎖存取 tooyour 目錄中的外部使用者。
>
>

如果使用者被刪除其主目錄中，或使用者取消其 Microsoft 帳戶，hello 外部使用者仍會存在目錄中。 不過，您的目錄中的 hello 使用者無法存取資源，因為它們無法使用的主目錄或 Microsoft 帳戶驗證。

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>目前支援讓 Azure AD 外部使用者存取的服務
* **Azure 傳統入口網站**： 可讓外部使用者管理員的多個目錄 toomanage 每個這些目錄。
* **SharePoint Online**： 如果已啟用外部共用，讓外部使用者 tooaccess SharePoint Online 授權資源。
* **Dynamics CRM**： 如果 hello 使用者已透過 PowerShell 授權，可讓外部使用者 tooaccess 授權 Dynamics CRM 中的資源。
* **Dynamics AX**： 如果 hello 使用者已透過 PowerShell 授權，可讓外部使用者 tooaccess 授權 Dynamics AX 中的資源。 hello 限制[Azure AD 的外部使用者](#known-limitations-of-azure-ad-external-users)tooexternal 使用者 Dynamics AX 中的也會套用。

## <a name="next-steps"></a>後續步驟
* [加入新使用者 tooAzure Active Directory](active-directory-create-users.md)
* [管理 Azure AD](active-directory-administer.md)
* [在 Azure AD 中管理密碼](active-directory-manage-passwords.md)
* [在 Azure AD 中管理群組](active-directory-manage-groups.md)
