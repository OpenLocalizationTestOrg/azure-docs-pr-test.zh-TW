---
title: "在 Azure Active Directory aaaManaging 群組 |Microsoft 文件"
description: "如何 toocreate 和管理群組 toomanage Azure 使用 Azure Active Directory 的使用者。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>在 Azure Active Directory 中管理群組
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-groups-create-azure-portal.md)
> * [Azure 傳統入口網站](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Hello 能力 toocreate 使用者群組的其中一個 hello Azure Active Directory (Azure AD) 使用者管理功能。 您使用群組 tooperform 管理工作，例如指派授權或權限的使用者 tooa 數目一次。 您也可以使用群組 tooassign 存取的權限

* 資源，例如 hello 目錄中的物件
* 資源外部 toohello 目錄，例如 SaaS 應用程式、 Azure 服務、 SharePoint 網站或內部部署資源

此外，資源擁有者也可以指派存取 tooa 資源 tooan Azure AD 群組由他人所擁有。 此指派會授與該群組存取 toohello 資源 hello 成員。 然後，hello hello 群組擁有者管理 hello 群組的成員資格。 實際上，hello 資源擁有者的委派 toohello 資源擁有者 hello 群組 hello 權限 tooassign 使用者 tootheir。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 Toomanage 群組的方式在 hello Azure AD 系統管理中心，請參閱[建立群組並新增 Azure Active Directory 中的成員](active-directory-groups-create-azure-portal.md)。

## <a name="how-do-i-create-a-group"></a>如何建立群組？
根據您組織已訂閱 hello 服務 toowhich，您可以建立使用 hello 下列其中一種群組：

* hello Azure 傳統入口網站
* hello Office 365 帳戶入口網站
* hello Windows Intune 帳戶入口網站

執行 hello Azure 傳統入口網站中，我們將說明的工作。 如需使用非 Azure 入口網站 toomanage Azure AD 目錄的詳細資訊，請參閱[管理 Azure AD 目錄](active-directory-administer.md)。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後選取 為您的組織 hello 目錄 hello 名稱。
2. 選取 hello**群組** 索引標籤。
3. 選取 [新增群組] 。
4. 在 hello**加入群組**視窗中，指定 hello 名稱和 hello 群組的描述。

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>如何新增或移除安全性群組中的個別使用者？
**tooadd 的個別使用者 tooa 群組**

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後選取 為您的組織 hello 目錄 hello 名稱。
2. 選取 hello**群組** 索引標籤。
3. 開啟您想要 tooadd 成員 hello 群組 toowhich。 開啟 hello**成員**hello 索引標籤上選取的群組，如果尚未顯示它。
4. 選取 [新增成員] 。
5. 在 hello**新增成員**頁面上，選取 hello hello 使用者或群組的名稱要 tooadd 為此群組的成員。 請確定這個名稱已加入 toohello**選取**窗格。

**tooremove 個別使用者從群組**

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後選取 為您的組織 hello 目錄 hello 名稱。
2. 選取 hello**群組** 索引標籤。
3. 開啟您想要從中 tooremove 成員 hello 群組。
4. 選取 hello**成員**索引標籤，選取 hello 成員名稱的 hello 您想要從這個群組中，tooremove，然後按一下**移除**。
5. 在 hello 提示字元中，確認您想 tooremove hello 群組從這個成員。

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>如何以動態方式管理 hello 群組成員資格？
在 Azure AD 中，您可以非常輕鬆地設定哪些使用者是 toobe 群組成員的 hello 簡單規則 toodetermine。 簡單的規則是指僅進行一項比較的規則。 例如，如果一個群組被指派 tooa SaaS 應用程式，您可以設定規則 tooadd 使用者職稱為 「 銷售代表 」。 此規則然後授與存取 toothis SaaS 應用程式 tooall 使用者具有該目錄中的職稱。

當使用者變更的任何屬性，hello 系統評估所有的動態群組規則目錄 toosee 如果 hello 使用者 hello 屬性變更會觸發任何群組中加入或移除。 如果使用者滿足群組中的規則，它們會新增為成員 toothat 群組。 如果它們不再滿足其所隸屬的群組的 hello 規則，則會從該群組移除做為成員。

> [!NOTE]
> 您可以為安全性群組或 Office 365 群組的動態成員資格設定規則。 群組為基礎的指派 tooapplications 目前不支援巢狀的群組成員資格。
>
> 群組動態成員資格要求指派給 Azure AD Premium 授權 toobe
>
> * 負責管理群組中的 hello 規則 hello 系統管理員
> * Hello 群組的所有成員
>
>

**tooenable 群組動態成員資格**

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後選取 為您的組織 hello 目錄 hello 名稱。
2. 選取 hello**群組**索引標籤，而且您想要 tooedit 開啟 hello 群組。
3. 選取 hello**設定**索引標籤，然後再設定**啟用動態成員資格**太**是**。
4. 設定 hello 群組 toocontrol 一個簡單的單一規則的這個群組的功能如何動態成員資格。 請確定 hello**新增使用者位置**選項已選取，然後選取 hello 清單 （例如，department、 jobTitle 等），從的 使用者屬性
5. 接著，選取一個條件 (不等於、等於、開頭不是、開頭為、不包含、包含、不符合、符合)。
6. 指定的比較值為 hello 選取的使用者內容。

有關如何 toolearn toocreate*進階*規則 （可以包含多個比較的規則） 的動態群組成員資格，請參閱[使用屬性 toocreate 進階規則](active-directory-accessmanagement-groups-with-advanced-rules.md)。

## <a name="additional-information"></a>其他資訊
這些文章提供有關 Azure Active Directory 的其他資訊。

* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [設定群組設定的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [什麼是 Azure Active Directory？](active-directory-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
