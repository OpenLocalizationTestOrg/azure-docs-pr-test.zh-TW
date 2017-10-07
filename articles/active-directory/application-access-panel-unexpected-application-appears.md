---
title: "hello 存取面板上出現 aaaHow 應用程式 |Microsoft 文件"
description: "應用程式會出現在 hello 存取面板進行疑難排解"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>應用程式如何 hello 存取面板上顯示

hello 存取面板是網頁型的入口網站，可讓使用者使用工作或學校帳戶，Azure Active Directory (Azure AD) tooview 並啟動雲端架構應用程式中的 hello Azure AD 系統管理員已授與它們存取權。 這些應用程式會代表 hello Azure AD 入口網站中的 hello 使用者設定。 hello 系統管理員可以佈建 hello 應用程式 toohello 使用者直接或 tooa 群組的使用者是導致 hello hello 使用者的存取面板上顯示的應用程式的一部分。

## <a name="general-issues-toocheck-first"></a>一般會先發出 toocheck

-   如果應用程式就已從使用者或群組 hello 使用者的成員，toosign 入和登出再試一次到 hello 使用者的存取面板後幾分鐘的時間 toosee 如果 hello 應用程式中移除。

-   授權就已從使用者或群組 hello 使用者隸屬這可能需要很長的時間，取決於 hello 大小和複雜度所做的變更 toobe hello 群組。 允許額外的時間才能登入存取面板 hello。

## <a name="problems-related-tooassigning-applications-toousers"></a>問題相關的 tooassigning 應用程式 toousers

使用者會看見應用程式存取面板上因為其已被先前指派 tooit。 以下是一些方式 toocheck:

-   [檢查 toohello 應用程式時，是否要指派使用者](#check-if-a-user-is-assigned-to-the-application)

-   [檢查是否授權使用者相關 toohello 應用程式](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>檢查 toohello 應用程式時，是否要指派使用者

toocheck 如果使用者被指派 toohello 應用程式，請遵循 hello 執行下列步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

6.  **搜尋**hello hello 有問題的應用程式名稱。

7.  按一下 [使用者和群組]。

8.  如果您的使用者被指派 toohello 應用程式，請檢查 toosee。

  * 如果您想從 hello 應用程式、 tooremove hello 使用者**按一下 hello 列**hello 使用者，然後選取**刪除**。

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>檢查是否授權使用者相關 toohello 應用程式

toocheck 使用者的指派授權，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下**授權**toosee 授權 hello 使用者目前已指派。

   * 如果這啟用第一個合作對象 Office 應用程式 tooappear tooan Office 授權指派給 hello 使用者 hello 使用者的存取面板。

## <a name="problems-related-tooassigning-applications-toogroups"></a>問題相關的 tooassigning 應用程式 toogroups

使用者會看見應用程式存取面板上因為它們已被指派 hello 應用程式群組的一部分。 以下是一些方式 toocheck:

-   [檢查使用者的群組成員資格](#check-a-users-group-memberships)

-   [檢查使用者是否 tooa 授權指派給群組的成員](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>檢查使用者的群組成員資格

toocheck 群組的成員資格，後續 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下 [群組]。

8.  如果您的使用者屬於群組的核取 toosee 指派 toohello 應用程式。

   * 如果您想從 hello 群組 tooremove hello 使用者**按一下 hello 列**hello 群組和選取的刪除。

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>檢查使用者是否 tooa 授權指派給群組的成員

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**使用者和群組**hello 瀏覽功能表中。

5.  按一下 [所有使用者]。

6.  **搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。

7.  按一下 [群組]。

8.  按一下 特定群組的 hello 資料列。

9.  按一下**授權**toosee 授權 hello 群組已指派 tooit。

  * 如果這可能會讓特定的第一個合作對象 Office 應用程式 tooappear tooan Office 授權指派給 hello 群組 hello 使用者的存取面板。


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>如果不執行 hello 這些疑難排解步驟解決 hello 問題

開啟支援票證以 hello 如果有的話，下列資訊：

-   相互關聯錯誤 ID

-   UPN (使用者電子郵件地址)

-   租用戶識別碼

-   瀏覽器類型

-   錯誤發生期間的時區和時間/時間範圍

-   Fiddler 追蹤

## <a name="next-steps"></a>後續步驟
[使用 Azure Active Directory 管理應用程式](active-directory-enable-sso-scenario.md)
