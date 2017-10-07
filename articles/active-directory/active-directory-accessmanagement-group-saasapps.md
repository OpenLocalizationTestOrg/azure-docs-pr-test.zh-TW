---
title: "aaaUsing 群組 toomanage 存取 tooSaaS 應用程式 |Microsoft 文件"
description: "如何在 Azure Active Directory Premium 或基本 tooassign toouse 群組存取 tooSaaS 應用程式與 Azure Active Directory 整合。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>使用群組 toomanage 存取 tooSaaS 應用程式
Azure AD Premium 或 Azure AD Basic 授權使用 Azure Active Directory (Azure AD)，您可以使用群組 tooassign 存取 tooa SaaS 應用程式與 Azure AD 整合。 比方說，如果您想 tooassign hello 行銷部門 toouse 五個不同 SaaS 應用程式的存取，您可以建立包含 hello 行銷部門中的 hello 使用者的群組，然後指派該群組 toothese 五個 SaaS 應用程式hello 行銷部門所需。 如此一來可以管理的行銷部門在同一個地方 hello hello 成員資格來節省時間。 然後會指派 toohello 應用程式會在新增為 hello 行銷群組成員，並有它們從 hello 行銷 群組中移除時從 hello 應用程式中移除其指派時。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 

這項功能可以搭配數百個您可以從新增 hello Azure AD 應用程式庫的應用程式。

**tooassign 群組 tooa SaaS 應用程式的存取權**

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**左側 hello hello 導覽列上。
2. 選取 hello**目錄**索引標籤，然後再開啟 hello 想 tooassign 群組 tooa SaaS 應用程式的存取權的目錄。
3. 選取 hello**應用程式** 索引標籤。選取您從 hello 應用程式庫新增應用程式，然後按一下hello**使用者和群組** 索引標籤。
4. 在 hello**使用者和群組**索引標籤上，在 hello**開頭**欄位中輸入 hello 名稱要的 hello 群組 toowhich tooassign 存取，然後選取 hello hello 右上角的核取記號。 您只需要 tootype hello 第一個部分群組的名稱。
5. 選取 hello 群組，然後再選取 [hello**指派存取權**] 按鈕。 選取**是**您看見 hello 確認訊息。 在此時間以群組為基礎的指派 tooapplications 不支援巢狀的群組成員資格。
6. 您也可以查看哪些使用者指派 toohello 應用程式，直接或透過群組成員資格。 toodo，變更 hello**顯示下拉式清單中，從 「 群組 」**太**「 所有使用者 」**。 hello 清單會顯示 hello 目錄和每個使用者指派 toohello 應用程式中的使用者。 hello 清單也會顯示是否要指派給 hello 分派使用者 toohello 的應用程式直接 （指派類型顯示為 直接），或依照群組成員資格 （指派類型顯示為 繼承'。）

> [!NOTE]
> 只在您啟用 Azure AD Premium 或 Azure AD Basic 之後，您可以看到 hello 使用者和群組 索引標籤。
>
>

### <a name="next-steps"></a>後續步驟
這些文章提供有關 Azure Active Directory 的其他資訊。

* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [設定群組設定的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [什麼是 Azure Active Directory？](active-directory-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
