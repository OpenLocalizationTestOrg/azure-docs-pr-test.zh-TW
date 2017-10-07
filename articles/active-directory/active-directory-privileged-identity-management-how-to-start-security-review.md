---
title: "aaaHow toostart 存取檢閱 |Microsoft 文件"
description: "了解如何 toocreate 存取檢閱特殊權限的身分識別與 hello Azure Privileged Identity Management 的應用程式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>如何 toostart 存取檢閱在 Azure AD Privileged Identity Management
當使用者擁有不再需要的特殊存取權時，角色指派就會變成「過時」。 在這些過時的角色指派與相關訂單 tooreduce hello 風險，特殊權限的角色系統管理員應該定期檢閱 hello 角色已獲得使用者。 本文件涵蓋 hello 存取檢閱啟動 Azure AD Privileged Identity Management (PIM) 中的步驟。

## <a name="start-an-access-review"></a>開始存取權檢閱
> [!NOTE]
> 如果您沒有在 hello Azure 入口網站中加入 hello PIM 應用程式 tooyour 儀表板，請參閱中的 hello 步驟[開始使用 Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)
> 
> 

從 hello PIM 應用程式主頁面上，有三種方式 toostart 存取檢閱：

* [存取權檢閱] > [新增]
* [角色] > [檢閱] 按鈕
* 選取 hello 特定角色 toobe 檢閱從 hello 角色清單 >**檢閱**按鈕

當您按一下 hello**檢閱**按鈕，hello**開始存取檢閱**刀鋒視窗隨即出現。 在這個刀鋒視窗中，您正在進行 tooconfigure hello 檢閱的名稱和時間限制選擇角色 tooreview，並且決定誰可以執行 hello 檢閱。

![開始存取權檢閱 - 螢幕擷取畫面][1]

### <a name="configure-hello-review"></a>設定 hello 檢閱
toocreate 存取檢閱，您需要 tooname 它並設為開始和結束日期。

![設定檢閱 - 螢幕擷取畫面][2]

請檢閱久，使用者 toocomplete hello hello 長度。 如果您完成 hello 結束日期之前，您可以一律停駐 hello 檢閱早期。

### <a name="choose-a-role-tooreview"></a>選擇角色 tooreview
每個檢閱只針對一個角色。 除非您從特定的角色 刀鋒視窗中啟動 hello 存取檢閱，您將現在需要 toochoose 角色。

1. 瀏覽過**檢視角色成員資格**
   
    ![檢閱角色成員資格 - 螢幕擷取畫面][3]
2. Hello 清單中選擇一個角色。

### <a name="decide-who-will-perform-hello-review"></a>決定誰可以執行 hello 檢閱
執行檢閱的選項有三個。 您可以指派 hello 檢閱 toosomeone else toocomplete，您可以自行操作，或您可以檢閱其本身存取每位使用者。

1. 瀏覽過**選取檢閱者**
   
    ![選取檢閱者 - 螢幕擷取畫面][4]
2. 選擇其中一個 hello 選項：
   
   * **選取檢閱者**︰如果您不知道誰需要存取權，請使用此選項。 使用此選項，您可以指派 hello 檢閱 tooa 資源擁有者或群組管理員 toocomplete。
   * **我**： 如果您想 toopreview 如何存取檢閱工作，或您想 tooreview 代表人員無法。
   * **成員檢閱本身**： 使用這個選項 toohave hello 使用者檢閱他們自己的角色指派。

### <a name="start-hello-review"></a>開始 hello 檢閱
最後，您擁有 hello 選項 toorequire 使用者提供的原因，如果他們同意其存取權。 如果需要，新增 hello 檢閱的描述，然後選取**啟動**。

請確定您讓使用者知道，正在等候存取檢閱，並顯示它們[如何 tooperform 存取檢閱](active-directory-privileged-identity-management-how-to-perform-security-review.md)。

## <a name="manage-hello-access-review"></a>管理 hello 存取檢閱
Hello 檢閱者完成 hello Azure AD PIM 儀表板中的檢視時，您可以追蹤 hello 進度，在 hello 存取檢閱 > 一節。 沒有存取權限將會變更在 hello 目錄，直到[hello 檢閱完成](active-directory-privileged-identity-management-how-to-complete-review.md)。

直到 hello 檢閱時間已經結束，您可以提醒使用者 toocomplete 他們檢閱，或停止 hello 檢閱早期 hello 存取從檢閱 > 一節。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>PIM 目錄
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
