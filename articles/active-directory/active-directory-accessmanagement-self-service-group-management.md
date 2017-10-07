---
title: "自助服務應用程式存取管理的 Azure Active Directory 註冊 aaaSetting |Microsoft 文件"
description: "自助式群組管理可讓使用者 toocreate 和管理安全性群組或 Azure Active Directory 並提供使用者 hello 可能性 toorequest 安全性群組或 Office 365 群組成員資格中的 Office 365 群組"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>設定 Azure Active Directory 進行自助服務群組管理
自助式群組管理可讓使用者 toocreate，以及管理安全性群組或 Azure Active Directory (Azure AD) 中的 Office 365 群組。 安全性群組或 Office 365 群組成員資格，也可以要求使用者，然後 hello hello 群組的擁有者可以核准或拒絕的成員資格。 如此一來，群組成員資格的日常控制權可以委派的 toopeople 對於了解該成員資格的 hello 商務內容。 自助式群組管理功能僅供安全性群組和 Office 365 群組使用，但具備郵件功能的安全性群組或通訊群組清單無法使用此功能。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。

自助式群組管理目前包含兩個重要案例：委派的群組管理和自助式群組管理。

* **委派群組管理**範例是管理存取 tooa SaaS 應用程式的 hello 公司使用的系統管理員。 管理這些存取權變得很麻煩，所以此系統管理員要求 hello 業務擁有者 toocreate 新的群組。 hello 系統管理員指派 hello 應用程式 toohello 新群組，請存取，並新增 toohello 群組已經存取 toohello 應用程式的所有人員。 hello 業務擁有者接著可以加入更多的使用者，以及這些使用者自動佈建的 toohello 應用程式。 hello 業務擁有者不需要 toowait 的 hello 管理員 toomanage 存取的使用者。 如果 hello 系統管理員授與 hello 相同的權限 tooa 管理員，在不同的商務群組中，則該人員也可以管理他們自己的使用者存取權。 Hello 業務擁有者都 hello 管理員可以檢視或管理其他人的使用者。 hello 系統管理員仍然可以看到所有的使用者具有存取 toohello 應用程式和視需要封鎖存取權限。
* **自助式群組管理** ：此案例的其中一個範例是都已獨立設定 SharePoint Online 網站的兩個使用者。 他們想 toogive 每個其他的小組存取 tootheir 站台。 tooaccomplish，他們可以在 Azure AD 中建立一個群組，並在 SharePoint Online 中每個選取的群組 tooprovide 存取 tootheir 站台。 若有人想要存取，他們要求從 hello 存取面板，並在核准之後他們存取 tooboth SharePoint Online 網站自動。 其中一個更新版本中，決定存取 hello 的站台的所有人也必須都取得存取 tooa 特定 SaaS 應用程式。 hello 的 hello SaaS 應用程式的系統管理員可以新增 hello 應用程式 toohello SharePoint Online 網站的存取權限。 從那時起，任何取得核准的要求提供存取 toohello 兩個 SharePoint Online 網站以及 toothis SaaS 應用程式。

## <a name="making-a-group-available-for-end-user-self-service"></a>提供可供一般使用者自助服務的群組
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，開啟您的 Azure AD 目錄。
2. 在 hello**設定**索引標籤上，設定**委派群組管理**tooEnabled。
3. 設定**使用者可以建立安全性群組**或**使用者可以建立 Office 群組**tooEnabled。

當**使用者可以建立安全性群組**已啟用，您的目錄中的所有使用者允許 toocreate 新的安全群組並加入成員 toothese 群組。 這些新的群組會也會顯示在所有其他使用者的 hello 存取面板中。 如果 hello hello 群組上的原則設定允許，其他使用者可以建立要求 toojoin 這些群組。 如果 [使用者可以建立安全性群組]  已停用，使用者就無法建立群組，也無法變更其擁有的現有群組。 不過，它們仍可以管理這些群組的 hello 成員資格及核准要求，從其他使用者 toojoin 其群組。

您也可以使用**可為安全性群組使用自助的使用者**tooachieve 更精細的存取控制，透過您的使用者的自助式群組管理。 當**使用者可建立群組**已啟用，您的目錄中的所有使用者允許 toocreate 新群組並加入成員 toothese 群組。 將**可為安全性群組使用自助的使用者**tooSome，您會限制群組管理 tooonly 有限的使用者群組。 當此參數設定 tooSome 時，您必須先新增使用者 toohello 群組 SSGMSecurityGroupsUsers，他們才能建立新群組並新增成員 toothem。 藉由設定**可為安全性群組使用自助的使用者**tooAll，您啟用目錄 toocreate 新群組中的所有使用者。

您也可以使用 hello**可為安全性群組使用自助的群組**方塊 toospecify 群組，其成員可使用自助功能的自訂名稱。

## <a name="next-steps"></a>後續步驟
這些文章提供有關 Azure Active Directory 的其他資訊。

* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [設定群組設定的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [什麼是 Azure Active Directory？](active-directory-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
