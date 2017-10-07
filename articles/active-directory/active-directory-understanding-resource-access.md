---
title: "在 Azure 中的存取 aaaUnderstanding 資源 |Microsoft 文件"
description: "本主題說明在 hello 中使用訂用帳戶系統管理員 toocontrol 資源存取相關的概念完整 Azure 入口網站"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>了解 Azure 中的資源存取
> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 hello Azure 入口網站提供[角色型存取控制](role-based-access-control-configure.md)因此可以更精確地管理 Azure 資源。
> 
> 

2013 年 10 月 hello Azure 傳統入口網站和服務管理 Api 與整合 Azure Active Directory 中順序 toolay hello 奠定改善管理存取 tooAzure 資源 hello 使用者經驗。 Azure Active Directory 已提供絕佳功能，例如使用者管理、內部部署目錄同步、Multi-Factor Authentication 和應用程式存取控制。 當然，這些也應該能夠用於全面管理 Azure 資源。

在 Azure 中從計費觀點著手的存取控制。 hello 擁有者的 Azure 帳戶，供造訪 hello [Azure 帳戶中心](https://account.windowsazure.com/subscriptions)，為 hello 帳戶系統管理員 (AA)。 訂用帳戶是帳單的容器，但也可做為安全性界限： 每個訂閱都有一個服務系統管理員 (SA)，可以加入、 移除和修改該訂用帳戶中的 Azure 資源使用 hello [Azure 傳統入口網站](https://manage.windowsazure.com/). 新的訂閱 hello 預設 SA 為 hello AA、 但是 hello AA 可以變更 hello Azure 帳戶中心中的 hello SA。

<br><br>![Azure 帳戶][1]

訂用帳戶也會與目錄產生關聯。 hello 目錄定義一組使用者。 這些可以是從 hello 工作或學校中建立 hello 目錄的使用者，或者可以是外部使用者 （也就是 Microsoft 帳戶）。 訂用帳戶都可以存取已獲指派為服務系統管理員 (SA) 或共同管理員 (CA); 這些目錄使用者子集hello 只例外狀況是，由於傳統原因，Microsoft 帳戶 (先前稱為 Windows Live ID) 可以指派為 SA 或 CA 不需要出現在 hello 目錄中。

<br><br>![Azure 中的存取控制][2]

Hello Azure 傳統入口網站中的功能可讓登入使用 Microsoft 帳戶 toochange hello 目錄使用 hello 訂用帳戶相關聯的 SAs**編輯目錄**命令 hello **訂閱**頁面**設定**。 請注意這項作業有 hello 該訂用帳戶的存取控制的影響。

> [!NOTE]
> hello**編輯目錄**中 hello Azure 傳統入口網站不使用 toousers 登入使用工作或學校帳戶，因為這些帳戶可以登入只有 toohello 目錄 toowhich 其所屬的命令。
> 
> 

<br><br>![簡單的使用者登入流程][3]

在 hello 簡單的情況下，組織 （例如 Contoso) 將會強制執行計費和 hello 相同的訂用帳戶設定存取控制。 也就是說，hello 目錄是由單一 Azure 帳戶所擁有的相關聯的 toosubscriptions。 成功登入 toohello Azure 傳統入口網站，使用者可以看到兩個集合的資源 （橙色 hello 上圖中所示）：

* 其使用者帳戶所在的目錄 (來自或加入為外部主體)。 請注意，用來登入該 hello 目錄不相關的 toothis 計算，因此無論您登入的地方，一律顯示您的目錄。
* 資源的訂用帳戶，會與用來登入的 hello 目錄相關聯，並且其中 hello 使用者屬於可存取 （當他們是 SA 或 CA）。

<br><br>![具有多個訂用帳戶和目錄的使用者][4]

具有跨多個目錄的使用者具有 hello 能力 tooswitch hello 目前內容 hello Azure 傳統入口網站使用 hello 訂用帳戶篩選。 在 hello 過程中，這會導致不同的登入 tooa 不同的目錄，但是這是透過單一登入 (SSO)。

在訂用帳戶之間移動資源等作業，可能會因為訂用帳戶的這個單一目錄檢視而變得更加困難。 tooperform hello 資源傳輸時，您可能需要 toofirst 使用 hello**編輯目錄**命令在 hello 訂閱] 頁面中**設定**tooassociate hello 訂閱 toohello 相同的目錄.

## <a name="next-steps"></a>後續步驟
* toolearn 深入了解如何 toochange 管理員 Azure 訂用帳戶，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)
* 如需有關 Azure Active Directory 與 tooyour Azure 訂用帳戶的關聯方式的詳細資訊，請參閱[都與 Azure Active Directory 相關聯 Azure 訂用帳戶](active-directory-how-subscriptions-associated-directory.md)
* 如需有關如何 tooassign 角色在 Azure AD 中，請參閱[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
