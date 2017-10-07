---
title: "aaaUse 群組在 Azure Active Directory toomanage 存取 tooresources |Microsoft 文件"
description: "如何在 Azure Active Directory toomanage 使用者 toouse 群組存取 tooon 內部部署和雲端應用程式和資源。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>使用 Azure Active Directory 群組管理存取 tooresources
Azure Active Directory (Azure AD) 是完整身分識別和存取管理解決方案，提供一組強固的功能 toomanage 存取 tooon 內部部署和雲端應用程式和資源包括如 Office 365 等 Microsoft online services 和許多非 Microsoft SaaS 應用程式。 本文章提供概觀，但如果您想使用 Azure AD 的 toostart 現在分組，請依照下列中的 hello 指示[在 Azure AD 中管理安全性群組](active-directory-accessmanagement-manage-groups.md)。 如果您想 toosee 如何使用 PowerShell toomanage 您可以深入了解 Azure Active directory 中的群組[群組管理的 Azure Active Directory cmdlet](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)。

> [!NOTE]
> toouse Azure Active Directory，您需要 Azure 帳戶。 如果您沒有帳戶，您可以 [註冊免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。
>
>

在 Azure AD 中，其中一個 hello 主要功能是 hello 能力 toomanage 存取 tooresources。 這些資源可以是 hello 目錄中，如同透過角色在 hello 目錄或外部 toohello 目錄，例如 SaaS 應用程式、 Azure services 和 SharePoint 網站或內部部署資源的權限 toomanage 物件 hello 案例的一部分資源。 有四種方式，可指定使用者存取權限 tooa 資源：

1. 直接指派

    可以將使用者指派直接 tooa 資源 hello 該資源的擁有者。
2. 群組成員資格

    群組只能指派 tooa 資源 hello 資源擁有者，並透過這種方式，授與該群組存取 toohello 資源 hello 成員。 Hello 群組的成員資格然後受 hello hello 群組擁有者。 實際上，hello 資源擁有者委派 hello 權限 tooassign 使用者 tootheir 資源 toohello 群組的擁有者 hello。
3. 以規則為基礎

    hello 資源擁有者可以使用規則 tooexpress 存取 tooa 資源應該指派的使用者。 hello 規則的 hello 結果取決於特定的使用者，該規則和它們的值中所使用的 hello 屬性和透過這種方式，hello 資源擁有者有效地委派 hello 右 toomanage 存取 tootheir 資源 toohello 授權來源 hellohello 規則中使用的屬性。 hello 資源擁有者仍管理 hello 規則本身，並決定哪些屬性和值提供存取 tootheir 資源。
4. 外部授權單位

    hello 存取 tooa 資源被衍生自外部來源;例如，從授權的來源，例如在內部部署目錄或例如 WorkDay 的 SaaS 應用程式同步處理群組。 hello 資源擁有者指派 hello 群組 tooprovide 存取 toohello 資源，並 hello 外部來源管理 hello hello 群組成員。

   ![存取管理圖表的概觀](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>觀看說明存取管理的影片
您可以在此觀賞說明與此相關的短片：

**Azure AD： 群組的簡介 toodynamic 成員資格**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>存取管理在 Azure Active Directory 中如何運作？
在 hello hello Azure AD 存取管理解決方案的中心是 hello 安全性群組。 使用安全性群組 toomanage 存取 tooresources 是知名的範例，可讓 hello 適合使用者群組的彈性且易於了解的方式 tooprovide 存取 tooa 資源。 hello 資源擁有者 （或 hello hello 目錄管理員） 可以指派群組 tooprovide 特定存取權限 toohello 資源他們所擁有。 hello 群組成員的 hello 提供 hello 存取和 hello 資源擁有者可以將委派的 else，例如部門經理或技術支援系統管理員群組 toosomeone hello 右 toomanage hello 成員清單。

![Azure Active Directory 存取管理圖表](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

hello 群組擁有者也可以讓該群組可供自助服務要求。 在此情況下，使用者可以搜尋和尋找 hello 群組，以要求 toojoin，有效地搜尋透過 hello 群組所管理的權限 tooaccess hello 資源。 hello hello 群組擁有者可以設定 hello 群組，以便自動核准加入要求，或需要 hello 群組的 hello 擁有者核准。 當使用者要求 toojoin 群組，hello 聯結要求轉送 toohello hello 群組擁有者。 如果其中 hello 擁有者核准 hello 要求，hello 提出要求的使用者會收到通知，而 hello 使用者是聯結的 toohello 群組。 如果其中 hello 擁有者拒絕 hello 要求，hello 提出要求的使用者會收到通知，但未加入 toohello 群組。

## <a name="getting-started-with-access-management"></a>開始使用存取管理
準備好 tooget 啟動嗎？ 您應該嘗試一些 hello 基本的工作，您可以使用 Azure AD 群組。 使用這些功能 tooprovide 特製化存取 toodifferent 一群人的組織中不同資源。 以下是基本的首要步驟清單。

* [建立簡單的規則群組 tooconfigure 動態成員資格](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [使用群組 toomanage 存取 tooSaaS 應用程式](active-directory-accessmanagement-group-saasapps.md)
* [提供可供一般使用者自助服務的群組](active-directory-accessmanagement-self-service-group-management.md)
* [使用 Azure AD Connect 的內部群組 tooAzure 正在同步處理](active-directory-aadconnect.md)
* [管理群組的擁有者](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>後續步驟
既然您已了解 hello 存取管理基本概念，以下是某些額外的進階的功能可用在 Azure Active Directory 中管理存取 tooyour 應用程式和資源。

* [使用屬性 toocreate 進階規則](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [在 Azure AD 中管理安全性群組](active-directory-accessmanagement-manage-groups.md)
* [在 Azure AD 中設定專用的群組](active-directory-accessmanagement-dedicated-groups.md)
* [群組的圖形 API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [設定群組設定的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
